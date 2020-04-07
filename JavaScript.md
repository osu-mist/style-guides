# JavaScript Style Guide ![Node.js](https://img.shields.io/badge/Node.js-10-brightgreen.svg) ![ECMAScript](https://img.shields.io/badge/ECMAScript-6-yellow.svg)

This is a style guide for writing code in JavaScript using Node.js. This includes all APIs created from the
[Express API Skeleton](https://github.com/osu-mist/express-api-skeleton).

## Airbnb Style Guide

As a base guide, the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) should be followed. Express
APIs enforce this by using [ESLint rules](https://github.com/osu-mist/express-api-skeleton/blob/master/.eslintrc.yml).

## Naming Conventions

When naming things using camel case such as variables or keys, **acronyms should not be capitalized**. If a single-letter
word is used such as "A" or "I", the word is capitalized and the word following it is also capitalized.

Example:

```js
const exampleJsonSerializer;
const osuId;
const idOsu;
const oracleDb;
const exampleOfAJsonSerializer;
```

## Documentation

Functions should be documented using [JSDoc](http://usejsdoc.org/) with a format similar to this example:

```js
/**
* @summary Checks if two strings are equal
* @function
* @param {string} paramA One string
* @param {string} paramB Another string
* @returns {boolean} true if strings are equal, false otherwise
* @throws Will throw an error if either parameter is falsy
*/
const function(paramA, paramB) {
  if (!paramA || !paramB) {
    throw new Error('Both strings must be non-empty');
  }
  return (paramA === paramB);
}
```

## Properties Spanning Multiple Lines

When listing more than 3 properties of an object, each property should be on its own line.

Example:

```js
const obj1 = { prop1, prop2, prop3 };

const obj2 = {
  prop1,
  prop2,
  prop3,
  prop4,
};
```

## Importing Modules

ES6 imports are preferred over commonjs `require` statements. However, for some situations such as
conditional imports, `require` should be used instead.

### Import Order

Whenever possible, the following should be grouped together, separated by a blank line at the top of a module in this
order:

1. `import` a third-party module

2. `import` a local module

3. `require` or use other method for importing module

4. Declare global variables and/or call functions

Each line within groups 1-3 should be ordered alphabetically by the first alphanumeric character in the name of the
package/file path in the statement.

Example:

```js
import a from 'a';
import b from 'b';

import * as file1 from './file1';
import { method } from './file2';

const c = someCondition ? require('c') : null;

const str = 'abc';
```

### Conditional Require Statements

From [ESLint's `global-require` rule](https://eslint.org/docs/rules/global-require#rule-details), a ternary require is allowed

Example from above link:

```js
var logger = DEBUG ? require('dev-logger') : require('logger');
```

or

```js
const package = packageIsNeeded ? require('package') : null;
```

## Nested Destructure Assignments

Nested destructure assignments can be done either by nesting curly braces or by destructuring properties of objects.

Example:

```js
const { b: { c } } = a;
```

or

```js
const { c } = a.b;
```
