# babel-plugin-web-dev-expression [![npm version](https://badge.fury.io/js/babel-plugin-web-dev-expression.svg)](https://badge.fury.io/js/babel-plugin-web-dev-expression)

A browser compatible fork of Facebook's dev-expression Babel plugin.

This plugin reduces or eliminates development checks from production code, but also works in a browser environment.
It defaults to a production environment in a browser.

## `__DEV__`

Replaces

```js
__DEV__
```

with

```js
typeof process != "object" ? false : !process.env ? false : process.env.NODE_ENV !== "production"
```

**Note:** The `dev-expression` transform does not run when `NODE_ENV` is `test`. As such, if you use `__DEV__`, you will need to define it as a global constant in your test environment.

## `invariant`

Replaces

```js
invariant(condition, argument, argument);
```

with

```js
if (!condition) {
  if (typeof process != "object" ? false : !process.env ? false : process.env.NODE_ENV !== "production") {
    invariant(false, argument, argument);
  } else {
    invariant(false);
  }
}
```

Recommended for use with https://github.com/zertosh/invariant or smaller https://github.com/alexreardon/tiny-invariant.

## `warning`

Replaces

```js
warning(condition, argument, argument);
```

with

```js
if (typeof process != "object" ? false : !process.env ? false : process.env.NODE_ENV !== "production") {
  warning(condition, argument, argument);
}
```

Recommended for use with https://github.com/r3dm/warning or smaller https://github.com/alexreardon/tiny-warning.
