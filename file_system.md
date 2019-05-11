# 8. File System 7%

## Open file

```js
fs.open(path, flags[, mode], callback)
```

Parameters:

`path` − This is the string having file name including path.

`flags` − Flags indicate the behavior of the file to be opened. All possible values have been mentioned below. (see also _File system flags_)

`mode` − It sets the file mode (permission and sticky bits), but only if the file was created. It defaults to 0666, readable and writeable.

`callback` − This is the callback function which gets two arguments (error, fileDescriptor)

### File descriptor

On POSIX systems, for every process, the kernel maintains a table of currently open files and resources. Each open file is assigned a simple numeric identifier called a _file descriptor_. At the system-level, all file system operations use these file descriptors to identify and track each specific file. Windows systems use a different but conceptually similar mechanism for tracking resources. To simplify things for users, Node.js abstracts away the specific differences between operating systems and assigns all open files a numeric file descriptor.

### File system flags

-   `'a'` - Open file for appending. The file is created if it does not exist.

-   `'ax'` - Like 'a' but fails if the path exists.

-   `'a+'` - Open file for reading and appending. The file is created if it does not exist.

-   `'ax+'` - Like 'a+' but fails if the path exists.

-   `'as'` - Open file for appending in synchronous mode. The file is created if it does not exist.

-   `'as+'` - Open file for reading and appending in synchronous mode. The file is created if it does not exist.

-   `'r'` - Open file for reading. An exception occurs if the file does not exist.

-   `'r+'` - Open file for reading and writing. An exception occurs if the file does not exist.

-   `'rs+'` - Open file for reading and writing in synchronous mode. Instructs the operating system to bypass the local file system cache.

This is primarily useful for opening files on NFS mounts as it allows skipping the potentially stale local cache. It has a very real impact on I/O performance so using this flag is not recommended unless it is needed.

This doesn't turn fs.open() or fsPromises.open() into a synchronous blocking call. If synchronous operation is desired, something like fs.openSync() should be used.

-   `'w'` - Open file for writing. The file is created (if it does not exist) or truncated (if it exists).

-   `'wx'` - Like 'w' but fails if the path exists.

-   `'w+'` - Open file for reading and writing. The file is created (if it does not exist) or truncated (if it exists).

-   `'wx+'` - Like 'w+' but fails if the path exists.

Other APIs:

-   ` fs.exists(path, callback)`` - - *deprecated* use `fs.access` instead
-   `fs.access(path[, mode], callback)` - tests a user's permissions for the file or directory specified by path
-   `fs.appendFile(path, data[, options], callback)`
-   `fs.chmod(path, mode, callback)` - changes the permissions of a file
-   `fs.chown(path, uid, gid, callback)` - change owner
-   `fs.close(fd, callback)` - use after `fs.open`
-   `fs.constants` - [fs constants](https://nodejs.org/dist/latest/docs/api/fs.html#fs_fs_constants_1)
-   `fs.copyFile(src, dest[, flags], callback)`
-   `fs.createReadStream(path[, options])`
-   `fs.createWriteStream(path[, options])`
-   `fs.link(existingPath, newPath, callback)` - creates a hard link between srcPath and dstPath. This is a way of creating many different paths to exactly the same file
-   `fs.mkdir(path[, options], callback)`
-   `fs.mkdtemp(prefix[, options], callback)` - creates a unique temporary directory
-   `fs.open(path[, flags[, mode]], callback)`
-   `fs.read(fd, buffer, offset, length, position, callback)` - use with `fs.open`
-   `fs.readdir(path[, options], callback)`
-   `fs.readFile(path[, options], callback)`
-   `fs.readlink(path[, options], callback)`
-   `fs.realpath(path[, options], callback)`
-   `fs.rename(oldPath, newPath, callback)`
-   `fs.rmdir(path, callback)`
-   `fs.stat(path[, options], callback)` - file stats
-   `fs.symlink(target, path[, type], callback)` - creates a symbolic link
-   `fs.truncate(path[, len], callback)` - truncates file
-   `fs.unlink(path, callback)` - removes file or link
-   `fs.utimes(path, atime, mtime, callback)` - change the file system timestamps of the object referenced by path
-   `fs.watch(filename[, options][, listener])` - watch for changes on filename, where `filename` is either a _file_ or a _directory_.
-   `fs.watchFile(filename[, options], listener)`
-   `fs.unwatchFile(filename[, listener])`
-   `fs.write(fd, buffer[, offset[, length[, position]]], callback)` - use with `fs.open`
-   `fs.write(fd, string[, position[, encoding]], callback)` - use with `fs.open`
-   `fs.writeFile(file, data[, options], callback)` -
