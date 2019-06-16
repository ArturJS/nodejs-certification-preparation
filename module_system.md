# 14. Module system (Scope) 6%

### How does `require` work?

Let's say we do `require('./awesome-module')`.

The resolution order is following:

1. `./awesome-module`
2. `./awesome-module.js`
3. `./awesome-module.json`
4. `./awesome-module.node`
5. `./awesome-module/index.js`
6. `./awesome-module/index.json`
7. `./awesome-module/index.node`
8. THROW "not found"

In case if we just do `require('awesome-module')` (only module name) it will try to find the module within

1. `./node_modules/awesome-module`
2. `../node_modules/awesome-module` - will go into parent directory
   ...
3. `<root_folder>/node_modules/awesome-module`
4. THROW "not found"

More detailed explanation can be found here https://github.com/nodejs/node/blob/master/doc/api/modules.md#all-together
