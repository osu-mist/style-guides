# JavaScript Style Guide

This is a style guide for writing code in JavaScript. This includes all APIs created from the
[Express API Skeleton](https://github.com/osu-mist/express-api-skeleton).

## Airbnb Style Guide

As a base guide, the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript) should be followed. Express
APIs enforce this by using [ESLint rules](https://github.com/osu-mist/express-api-skeleton/blob/master/.eslintrc.yml).

## Requiring Modules

Whenever possible, the following should be grouped together, separated by a blank line at the top of a module in this
order:

1. Require an NPM package

2. Require a local file

3. Use a require-like method such as `app-root-path`'s require function

4. Declare global variables or call functions

Each line within groups 1-3 should be ordered alphabetically by the first alphanumeric character in the name of the
package/file in the statement.

Example:

```js
const a = require('a');
const appRoot = require('app-root-path');
const b = require('b');

const file = require('./file');
const file2 = require('./file2');

const file3 = appRoot.require('dir/file3');
const file4 = appRoot.require('dir/file4');

const str = 'abc';
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

## Properties Spanning Multiple Lines

When listing more than 3 properties of an object, each property should be on its own line.

Example:

```js
const obj = { prop1, prop2, prop3 };

const obj2 = {
  prop1,
  prop2,
  prop3,
  prop4,
};
```
