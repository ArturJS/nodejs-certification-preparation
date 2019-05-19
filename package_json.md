# 11. Package.json 5%

-   `name`

-   `version` - must be parseable by https://github.com/npm/node-semver

-   `description` - will be displayed in `npm search`

-   `keywords` - helps to find via `npm search`

-   `homepage` - project url

-   `bugs` - url string or

```
{
    "url" : "https://github.com/owner/project/issues","email" : "project@hostname.com"
}
```

If a url is provided, it will be used by the `npm bugs` command.

-   license

-   people fields: `author`, `contributors` - The `“author”` is one person. `“contributors”` is an array of people.

```
{
    "name" : "Barney Rubble", // is required
    "email" : "b@rubble.com",
    "url" : "http://barnyrubble.tumblr.com/"
}
```

-   `files` - files to be included when your package is installed as a dependency

-   `main` - file which is entrypoint to your program

-   `browser` - is a hint to javascript bundlers or component tools when packaging modules for client side use. See also https://github.com/defunctzombie/package-browser-field-spec .

-   `bin` - path to \*.js for running in CLI

-   `man` - path to docs

-   `directories`

```
{
    "bin": "./bin", // use for adding all the files in an existing bin directory
    "doc": "./doc", // Put markdown files in here.
    "lib": "./lib", // where is most of files of your library, it’s useful meta info.
    "man": "./man", // A folder that is full of man pages.
    "example": "./example", // Put example scripts in here.
    "test": "./test" // Put your tests here
},
```

-   `repository` - Specify the place where your code lives. If the git repo is on GitHub, then the `npm docs` command will be able to find you.

-   `scripts` - for `npm run [script_name]`. See also https://docs.npmjs.com/misc/scripts

-   `config` - set configuration parameters used in package scripts that persist across upgrades https://docs.npmjs.com/files/package.json.html#config

-   `dependencies` - a simple object that maps a package name to a version range https://docs.npmjs.com/files/package.json.html#dependencies

-   devDependencies - the same but for development purpuses (will NOT be installed in `npm install --production`)

-   `peerDependencies` - list of dependencies that should be installed separately.

-   `bundleddependencies` - an array of package names that will be bundled when publishing the package.

-   `optionaldependencies`

-   `engines` - You can specify the version of node that your stuff works on:

```
{ "engines" : { "node" : ">=0.10.3 <0.12" } }
```

or npm:

```
{ "engines" : { "npm" : "~1.0.20" } }
```

-   `engineStrict` - This feature was removed in npm 3.0.0

-   `os` - specify which operating systems your module will run on:

```
"os" : [ "darwin", "linux" ]
```

with `"!"` you can exclude

```
"os" : [ "!win32" ]
```

-   `cpu` - the same as `os` but `cpu`)

-   `preferGlobal` - prefer `--global` installation

-   `private` - if `true` then npm will refuse to publish it.

-   `publishConfig` - config values that will be used at publish-time.

### Default values

https://docs.npmjs.com/files/package.json.html#default-values

-   `"scripts": { "start": "node server.js" }`
-   `"scripts": { "install": "node-gyp rebuild" }`
