# 2. Diagnostics (Basics, Debugging, Performance) 5%

<hr>

### Performance profiling with `perf` and `0x`

**perf**

-   `apt-get install linux-tools-common linux-tools-generic linux-tools-$(uname -r)`
-   `node --perf_basic_proof_only_functions server.js`
-   `perf record -F 99 -p <pid> -g -- sleep 30` - take 99 stack trace snapshots every second during 30 seconds
-   `perf script > stacks.out`

**0x**

-   `npm install 0x -g`
-   `0x -c gen stacks.out > flamegraph.html`

<hr>

### Coredump generation on `Uncaught exception` with `llnode` inspecting

1. In order to generate coredump

```
ulimit -c unlimited # to allow coredump generation
node --abort-on-uncaught-exception server.js # it will generate coredump on uncaught exception
```

Coredump will be created either in `/cores` folder or in current folder.

2. Install `llnode`

```
apt search lldb # find available versions
# in my case I installed 6.0 version
sudo apt install lldb-6.0 python-lldb-6.0 liblldb-6.0-dev
sudo ln -s /usr/bin/lldb-6.0 /usr/bin/lldb
npm i -g llnode
```

3. Inspect coredump

```
llnode -c <path to coredump file>
```

for example

```
llnode -c core # open coredump file from current folder
```

then it will open `llnode` terminal ([q] + [Enter] to exit)

```
v8 help #show all commands
```

More information about how to work with llnode here -> https://developer.ibm.com/node/2016/08/15/exploring-node-js-core-dumps-using-the-llnode-plugin-for-lldb/

<hr>

### Memory leaks inspection with `heapdump`

App

```
npm install --save heapdump

require('heapdump')
```

Production server

```
kill -USR2 <pid>
```

Google Chrome DevTools

```
profiles -> Load (2 dumps) -> Comparison
```

#### Common causes of memory leaks:

1. Frequent garbage collections **Scavenge GC** in **New Object Space** which loads CPU:

    - Expensive operations of `clone` and `merge` of objects
    - Frequent objects creation

2. **Old Object Space**

    - Closures
    - Timers

3. **Large Object Space**
    - JSON stringify and parse
    - strings concatenation

<hr>

### Debugging via chrome devtools

```
node --inspect server.js
```

<br>

or if you want to break on the first line of the application code

```
node --inspect-brk server.js
```

But I'm personally a big proponent of https://github.com/GoogleChromeLabs/ndb
