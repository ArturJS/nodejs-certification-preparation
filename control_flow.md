# 9. Control flow (Async tasks, Callbacks) 10%

#### Event Loop Briefly

```
   ┌───────────────────────────┐
┌─>│           timers          │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           poll            │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │           check           │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │
   └───────────────────────────┘
```

-   **timers** - `setTimeout()` and `setInterval()`
-   \*\* \*\* - completed or errored I/O operation to be executed here
-   **idle** - perform some libuv internal stuff (only used internally)
-   **prepare** - perform some preparation work before polling for I/O (only used internally)
-   **poll** - retrieve new I/O events; execute I/O related callbacks (almost
    all with the exception of close callbacks, the ones scheduled by timers,
    and `setImmediate()`); node will block here when appropriate.
-   **check** - `setImmediate()` callbacks are invoked here.
-   **close callbacks**: some close callbacks, e.g. `socket.on('close', ...)`.

Between each run of the event loop, Node.js checks if it is waiting for any asynchronous I/O or timers and shuts down cleanly if there are not any.

#### Phases in Detail

#### Timers

A timer specifies the threshold after which a provided callback **may be** executed.
Not early than after specified time.
(**NOT** in the exact time)

Fires only 1 timer per 1 event loop cycle.
(**NOT** all in once)

#### Pending callbacks

This phase executes callbacks for some system operations such as types of TCP errors. For example if a TCP socket receives `ECONNREFUSED` when attempting to connect, some \*nix systems want to wait to report the error. This will be queued to execute in the **pending callbacks** phase.

#### Idle, prepare - only used internally

#### Poll

The **poll** phase has two main functions:

1. Calculating how long it should block and poll for I/O, then
2. Processing events in the **poll** queue.

When the event loop enters the **poll** phase _and there are no timers
scheduled_, one of two things will happen:

-   _If the **poll** queue **is not empty**_, the event loop will iterate
    through its queue of callbacks executing them synchronously until
    either the queue has been exhausted, or the system-dependent hard limit
    is reached.

-   _If the **poll** queue **is empty**_, one of two more things will
    happen:

    -   If scripts have been scheduled by `setImmediate()`, the event loop
        will end the **poll** phase and continue to the **check** phase to
        execute those scheduled scripts.

    -   If scripts **have not** been scheduled by `setImmediate()`, the
        event loop will wait for callbacks to be added to the queue, then
        execute them immediately.

Once the **poll** queue is empty the event loop will check for timers _whose time thresholds have been reached_. If one or more timers are ready, the event loop will wrap back to the **timers** phase to execute those timers' callbacks.

#### Check

This phase allows a person to execute callbacks immediately after the **poll** phase has completed. If the **poll** phase becomes idle and scripts have been queued with `setImmediate()`, the event loop may continue to the **check** phase rather than waiting.

`setImmediate()` is actually a special timer that runs in a separate phase of the event loop. It uses a libuv API that schedules callbacks to execute after the **poll** phase has completed.

Generally, as the code is executed, the event loop will eventually hit the **poll** phase where it will wait for an incoming connection, request, etc. However, if a callback has been scheduled with `setImmediate()` and the **poll** phase becomes idle, it will end and continue to the **check** phase rather than waiting for **poll** events.

#### Close callbacks

If a socket or handle is closed abruptly (e.g. `socket.destroy()`), the `'close'` event will be emitted in this phase. Otherwise it will be emitted via `process.nextTick()`.

<br>

#### `setImmediate()` vs `setTimeout()`

`setImmediate()` and `setTimeout()` are similar, but behave in different ways depending on when they are called.

-   `setImmediate()` is designed to execute a script once the
    current **poll** phase completes.
-   `setTimeout()` schedules a script to be run after a minimum threshold
    in ms has elapsed.

If we run the following script which is not within an I/O cycle (i.e. the main module), the order in which the two timers are executed is **non-deterministic**, as it is bound by the performance of the
process:

```js
// timeout_vs_immediate.js
setTimeout(() => {
    console.log('timeout');
}, 0);

setImmediate(() => {
    console.log('immediate');
});
```

```
$ node timeout_vs_immediate.js
timeout
immediate

$ node timeout_vs_immediate.js
immediate
timeout
```

However, if you move the two calls within an I/O cycle, the `setImmediate` callback **is always executed first**:

```js
// timeout_vs_immediate.js
const fs = require('fs');

fs.readFile(__filename, () => {
    setTimeout(() => {
        console.log('timeout');
    }, 0);
    setImmediate(() => {
        console.log('immediate');
    });
});
```

```
$ node timeout_vs_immediate.js
immediate
timeout

$ node timeout_vs_immediate.js
immediate
timeout
```

#### `process.nextTick()` with `Promise`-es will be called all in once between event loop phases. (as they are microtasks)
