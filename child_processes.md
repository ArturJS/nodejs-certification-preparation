# 5. Child Processes (Basics, no IPC/fork) 7%

## Spawn vs Fork vs Exec

-   `require('child_process').spawn();` - large data, stream, NOT a new V8 instance
-   `require('child_process').fork();` - new V8 instance, multiple workers
-   `require('child_process').exec();` - buffer, async, all the data at once

## Spawn

### Example

```js
const { spawn } = require('child_process');

spawn('node', 'program.js').stdout.on('data', data => {
    console.log('stdout: ' + data);
});
```

## Fork

### Example

```js
const { fork } = require('child_process');

fork('program.js').stdout.on('data', data => {
    console.log('stdout: ' + data);
});
```

## Exec

### Example

```js
const { exec } = require('child_process');

exec('node program.js', (error, stdout, stderr) => {
    if (error) console.log(error.code);
});
```
