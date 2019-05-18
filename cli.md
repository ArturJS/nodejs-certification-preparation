# 10. CLI (-e, -r, etc.) 3%

### Usage:

`node [options][ -e script | script.js | - ] [arguments]`

`node inspect script.js [arguments]`

`[arguments]` - will be available in `process.argv` as an array

### Options:

`-v, --version` print Node.js version

`-e, --eval` script evaluate script

`-p, --print` evaluate script and print result

`-c, --check` syntax check script without executing

`-i, --interactive` always enter the REPL even if stdin does not appear to be a terminal

`-r, --require` module to preload (option can be repeated)

`-` script read from stdin (default; interactive mode if a tty)

`--inspect[=[host:]port]` activate inspector on host:port (default: 127.0.0.1:9229)

`--inspect-brk[=[host:]port]` activate inspector on host:port and break at start of user script

`--inspect-port=[host:]port` set host:port for inspector

`--no-deprecation` silence deprecation warnings

`--trace-deprecation` show stack traces on deprecations

`--throw-deprecation` throw an exception on deprecations

`--pending-deprecation` emit pending deprecation warnings

`--no-warnings` silence all process warnings

`--napi-modules` load N-API modules (no-op - option kept for compatibility)

`--abort-on-uncaught-exception` aborting instead of exiting causes a core file to be generated for analysis

`--trace-warnings` show stack traces on process warnings

`--redirect-warnings=file` write warnings to file instead of stderr

`--trace-sync-io` show stack trace when use of sync IO is detected after the first tick

`--force-async-hooks-checks` enables checks for async_hooks

`--trace-events-enabled` track trace events

`--trace-event-categories` comma separated list of trace event categories to record

`--track-heap-objects` track heap object allocations for heap snapshots

`--prof-process` process v8 profiler output generated using `--prof`

`--zero-fill-buffers` automatically zero-fill all newly allocated `Buffer` and `SlowBuffer` instances

`--v8-options` print v8 command line options

`--v8-pool-size=num` set v8's thread pool size

`--tls-cipher-list=val` use an alternative default TLS cipher list

`--use-bundled-ca` use bundled CA store (default)

`--use-openssl-ca` use OpenSSL's default CA store

`--openssl-config=file` load OpenSSL configuration from the specified file (overrides OPENSSL_CONF)

`--icu-data-dir=dir` set ICU data load path to dir (overrides NODE_ICU_DATA)

`--preserve-symlinks` preserve symbolic links when resolving

`--experimental-modules` experimental ES Module support and caching modules

### Environment variables:

`NODE_DEBUG ','` separated list of core modules that should print debug information

`NODE_DISABLE_COLORS` set to 1 to disable colors in the REPL

`NODE_EXTRA_CA_CERTS` path to additional CA certificates file

`NODE_ICU_DATA` data path for ICU (Intl object) data (ICU - International Components for Unicode)

`NODE_NO_WARNINGS` set to 1 to silence process warnings

`NODE_NO_HTTP2` set to 1 to suppress the http2 module

`NODE_OPTIONS` set CLI options in the environment via a space-separated list

`NODE_PATH ':'`-separated list of directories prefixed to the module search path

`NODE_PENDING_DEPRECATION` set to 1 to emit pending deprecation warnings

`NODE_REPL_HISTORY` path to the persistent `REPL` history file

`NODE_REDIRECT_WARNINGS` write warnings to path instead of `stderr`

`OPENSSL_CONF` load OpenSSL configuration from file
