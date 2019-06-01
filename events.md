# 4. Events 9%

The `EventEmitter` class is defined and exposed by the events module:

```js
const EventEmitter = require('events');
```

#### Built-in events

`newListener` - is emitted **before** a listener is added to its internal array of listeners.

`removeListener` - is emitted **after** the listener is removed.

`error` - is emitted when an error occurs within an `EventEmitter` instance.
If an `EventEmitter` does **not** have at least one listener registered for the 'error' event, and an 'error' event is emitted, the error is thrown, a stack trace is printed, and the Node.js process exits.

```js
const myEmitter = new MyEmitter();
myEmitter.emit('error', new Error('whoops!'));
// Throws and crashes Node.js
```

#### Methods

-   `addListener`, `on` - adds a listener at the end of the listeners array for the specified event. **No checks** are made to see if the listener **has already been added**. Multiple calls passing the same combination of event and listener will result in the listener being added multiple times. Returns emitter, so calls **can be chained**.

-   `once(eventName, listener)` - adds a **one-time** listener function for the event named eventName. The next time eventName is triggered, this listener is removed and then invoked.

-   `removeListener`, `off` - removes a listener from the listener array for the specified event. Caution − It changes the array indices in the listener array behind the listener. `removeListener` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified event, then `removeListener` must be called multiple times to remove each instance. Returns emitter, so calls **can be chained**.

-   `removeAllListeners(eventName)` - removes all listeners, or those of the specified event

-   `emit(eventName[, ...args])` - **synchronously** calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each. Returns `true` if the event had listeners, `false` otherwise.

-   `eventNames()` - returns an array listing the events for which the emitter has registered listeners. The values in the array will be strings or `Symbols`.

-   `getMaxListeners()` - returns the current max listener value for the EventEmitter which is either set by `emitter.setMaxListeners(n)` or defaults to `EventEmitter.defaultMaxListeners`.

-   `listenerCount(eventName)` - returns the number of listeners listening to the event named `eventName`.

-   `listeners(eventName)` - returns a copy of the array of listeners for the event named `eventName`.

#### Misc

`EventEmitter.defaultMaxListeners` - By default, a maximum of **10** listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for all EventEmitter instances, the `EventEmitter.defaultMaxListeners` property can be used. If this value is not a positive number, a `TypeError` will be thrown. Take caution when setting the `EventEmitter.defaultMaxListeners` because the change **affects all EventEmitter instances**, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `EventEmitter.defaultMaxListeners`.
