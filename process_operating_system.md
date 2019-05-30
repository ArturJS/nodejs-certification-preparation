# 15. Process/Operating System (no IPC) 5%

## Process Module

The `process` object is an instance of `EventEmitter`.

#### Events

`beforeExit` - is emitted when Node.js empties its event loop and has no additional work to schedule.

`disconnect` - is emitted when the IPC channel is closed.

`exit` - is emitted when the Node.js process is about to exit as a result of either: `process.exit()` or event loop no longer having any additional work to perform.

`message` - If the Node.js process is spawned with an IPC channel (see the Child Process and Cluster documentation), the 'message' event is emitted whenever a message sent by a parent process using childprocess.send() is received by the child process.

`multipleResolves` - The 'multipleResolves' event is emitted whenever a Promise has been either:

-   Resolved more than once.
-   Rejected more than once.
-   Rejected after resolve.
-   Resolved after reject.

`rejectionHandled`

`uncaughtException`

`unhandledRejection`

`warning` - is emitted whenever Node.js emits a process warning.

#### Properties

`stdout` - A Writable Stream to stdout.

`stderr` - A Writable Stream to stderr.

`stdin` - A Writable Stream to stdin.

`argv` - An array containing the command line arguments. The first element will be 'node'

`execPath` - This is the absolute pathname of the executable that started the process.

`execArgv` - This is the set of node-specific command line options from the executable that started the process.

`env` - An object containing the user environment.

`exitCode` - A number which will be the process exit code

`version` - A compiled-in property that exposes NODE_VERSION.

`versions` - A property exposing the version strings of node and its dependencies.

`config` - An Object containing the JavaScript representation of the configure options that were used to compile the current node executable. This is the same as the "config.gypi" file that was produced when running the ./configure script.

`pid` - The PID of the process.

`title` - Getter/setter to set what is displayed in 'ps'.

`arch` - What processor architecture you're running on: 'arm'

`platform` - What platform you're running on: 'darwin'

`mainModule` - Alternate way to retrieve require.main. The difference is that if the main module changes at runtime

#### Methods

`abort()` - It causes the node to emit an abort. It causes the node to exit and generate a core file.

`chdir(directory)` - Changes the current working directory of the process or throws an exception if that fails.

`cwd()` - Returns the current working directory of the process.

`exit([code])` - Ends the process with the specified code. If omitted

`getgid()` - Gets the group identity of the process. This is the numerical group id

`setgid(id)` - Sets the group identity of the process. (See setgid(2)). It accepts either a numerical ID or a groupname string. If a groupname is specified

`getuid()` - Gets the user identity of the process. This is the numerical id

`setuid(id)` - Sets the user identity of the process (See setgid(2)). It accepts either a numerical ID or a username string. If a username is specified

`getgroups()` - Returns an array with the supplementary group IDs. POSIX leaves it unspecified if the effective group ID is included

`setgroups(groups)` - Sets the supplementary group IDs. This is a privileged operation

`initgroups(user, extra_group)` - Reads /etc/group and initializes the group access list, using all the groups of which the user is a member. This is a privileged operation, which implies that you have to be at the root or have the CAP_SETGID capability. This function is available only on POSIX platforms (i.e. not Windows, Android).

`kill(pid[, signal])` - Send a signal to a process. pid is the process id and signal is the string describing the signal to send. Signal names are strings like `'SIGINT'` or `'SIGHUP'`. If omitted, the signal will be `'SIGTERM'`.

`memoryUsage()` - Returns an object describing the memory usage of the Node process measured in bytes.

`nextTick(callback)` - Once the current event loop turn runs to completion

`umask([mask])` - Sets or reads the process's file mode creation mask. Child processes inherit the mask from the parent process. Returns the old mask if mask argument is given

`uptime()` - Number of seconds Node has been running.

`hrtime()` - Returns the current high-resolution real time in a [seconds

## OS Module

`arch()` - Returns the operating system CPU architecture

`constants` - Returns an object containing the operating system's constants for
process signals, error cotes etc.

`cpus()` - Returns an array containing information about the computer's CPUs

`endiannes()` - Returns the endianness of the CPU

`EOL` - Returns the end-of-line marker for the current
operating system

`freemem()` - Returns the number of free memory of the system

`hostname()` - Returns the hostname of the operating system

`loadavg()` - Returns an array containing the load averages, (1,
5, and 15 minutes)

`networkInterfaces()` - Returns the network interfaces that has a network
address

`platform()` - Returns information about the operating system's
platform

`release()` - Returns information about the operating system's
release

`tmpdir()` - Returns the operating system's default directory
for temporary files

`totalmem()` - Returns the number of total memory of the system

`type()` - Returns the name of the operating system

`uptime()` - Returns the uptime of the operating system, in
seconds

`userInfo()` - Returns information about the current user
