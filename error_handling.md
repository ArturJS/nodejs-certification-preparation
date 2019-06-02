# 7. Error Handling 7%

#### Four ways to to deliver an error in Node.js:

1. `throw` the error (making it an exception).
2. pass the error to a `callback` as a **first** argument (here `callback` is a function provided specifically for handling errors and the results of asynchronous operations)
3. pass the error to a `reject` Promise function
4. emit an `"error"` event on an EventEmitter

#### Operational errors vs. programmer errors

-   **Operational errors** represent run-time problems experienced by correctly-written programs. These are **NOT bugs** in the program. In fact, these are usually problems with something else:

    -   the system itself (e.g., out of memory or too many open files),
    -   the system's configuration (e.g., no route to a remote host), the network (e.g., socket hang-up), or a remote service (e.g., a 500 error, failure to connect, or the like).

    Examples include:

    -   failed to connect to server
    -   failed to resolve hostname
    -   invalid user input
    -   request timeout
    -   server returned a 500 response
    -   socket hang-up
    -   system is out of memory

-   **Programmer errors** are **bugs** in the program. These are things that can always be avoided by changing the code. They can never be handled properly (since by definition the code in question is broken).
    -   tried to read property of "undefined"
    -   called an asynchronous function without a callback
    -   passed a "string" where an object was expected
    -   passed an object where an IP address string was expected

#### Handling operational errors

-   Deal with the failure directly.
-   Propagate the failure to your client.
-   Retry the operation. (If you're going to retry, you should clearly document that you may retry multiple times, how many times you'll try before failing, and how long you'll wait between retries. Also, don't assume that you should always retry an operation.)
-   Blow up.
-   Log the error — and do nothing else.

#### (Not) handling programmer errors

**The best way to recover from programmer errors is to crash immediately and create core dump file.**

#### Specific recommendations for writing new functions

1. Be clear about what your function does.

    - what arguments it expects
    - the types of each of those arguments
    - any additional constraints on those arguments (e.g., must be a valid IP address)

2. Use Error objects (or subclasses) for all errors, and implement the Error contract.

    - All of your errors should either use the Error class or a subclass of it. You should provide name and message properties, and stack should work too (and be accurate).

3. Use the Error's `name` property to distinguish errors programmatically.
4. Augment the Error object with properties that explain details.
   At the very least, you want:

    - `name`: used to programmaticaly distinguish between broad types of errors (e.g., illegal argument vs. connection failed)
    - `message`: a human-readable error message.
    - `stack`: stack trace

5. If you pass a lower-level error to your caller, consider wrapping it instead.

**Bad**

```
myserver: Error: connect ECONNREFUSED
```

**Good**

```
myserver: failed to load configuration: connection refused from database at
127.0.0.1 port 1234.
```

#### Misc

For more information see also https://www.joyent.com/node-js/production/design/errors
