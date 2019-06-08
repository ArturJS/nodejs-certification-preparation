# 12. Javascript Prerequisites (Closures, prototypes, var/let/const) 6%

## Closure

**Closure** is a function having access to the parent scope, even after the parent function has closed.

## var, let, const

### var

1. **hoisting** - `var` declarations, wherever they occur, are processed before any code is executed.

2. scope - is its **current execution context**, which is either the enclosing **function or**, for variables declared outside any function, **global**. If you re-declare a JavaScript variable, it will not lose its value.

#### The differences between declared and undeclared variables are:

1. Declared variables are constrained in the execution context in which they are declared. Undeclared variables are always global.

2. Declared variables are created before any code is executed. Undeclared variables do not exist until the code assigning to them is executed.

3. Declared variables are a non-configurable property of their execution context (function or global). Undeclared variables are configurable (e.g. can be deleted).

### let

1. Scope - only within block `{...}`.
2. Cannot be redeclared in current block.
3. When declaring a variable in a loop for (let ...) - it is visible only in this loop. And each iteration has its own let variable.
4. Temporal dead zone - cannot be accessed before initialization. (otherwise `ReferenceError: Cannot access '<variable name>' before initialization`)

### const

The same as `let` except cannot be reassigned.

## Prototype

The prototype is the *“backup storage of properties and methods”* of an object that is automatically used during a search. Also it's a better place for object methods as they are **shared** between object instances.

**\_\_proto\_\_** - field on object that points to its prototype