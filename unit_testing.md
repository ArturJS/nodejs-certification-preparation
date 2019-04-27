# 1. Unit Testing 5%

## The Anatomy of a Unit Test:

1. **Arrange** - test setup
2. **Act** - calling the tested method
3. **Assert** - comparing with right result

<br>

## Modules Used for Node.js Unit Testing:

-   test runner: [mocha](https://www.npmjs.com/package/mocha), [tape](https://www.npmjs.com/package/tape), [jasmine](https://www.npmjs.com/package/jasmine), [karma](https://www.npmjs.com/package/karma), [jest](https://www.npmjs.com/package/jest)
-   assertion library: [chai](https://www.npmjs.com/package/chai), alternatively the [assert](https://nodejs.org/api/assert.html) module (for asserting)
-   test spies, stubs and mocks: [sinon](https://www.npmjs.com/package/sinon) (for test setup).

<br>

## Spies, stubs and mocks - which one and when?

1. **Spies** - you can use spies to get information on function calls, like how many times they were called, or what arguments were passed to them.
2. **Stubs** - stubs are like spies, but they replace the target function. You can use stubs to control a method's behaviour to force a code path (like throwing errors) or to prevent calls to external resources (like HTTP APIs).
3. **Mocks** - mock is a fake method with a pre-programmed behavior and expectations.

### Stubs VS Mocks

**Stubs** are dummy and always return hard-coded value whereas **Mocks** are usually configurable and comes with some internal implementation (for testing purposes).
