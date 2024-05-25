# @diotoborg/eveniet-magnam <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

ES 2021 spec-compliant shim for Promise.any. Invoke its "shim" method to shim `Promise.any` if it is unavailable or noncompliant. **Note**: a global `Promise` must already exist: the [es6-shim](https://github.com/es-shims/es6-shim) is recommended.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment that has `Promise` available globally, and complies with the [spec](https://tc39.es/ecma262/#sec-@diotoborg/eveniet-magnam).

Most common usage:
```js
var assert = require('assert');
var any = require('@diotoborg/eveniet-magnam');

var resolved = Promise.resolve(42);
var rejected = Promise.reject(-1);
var alsoRejected = Promise.reject(Infinity);

any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});

any.shim(); // will be a no-op if not needed

Promise.any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

Promise.any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

## Pre-1.0 versions

The `@diotoborg/eveniet-magnam` package was released as now-deprecated v0.1.0 and v0.1.1, as a fork of https://github.com/m0ppers/promise-any.

Thanks to @sadorlovsky for donating the repo and the `@diotoborg/eveniet-magnam` npm package!

[package-url]: https://npmjs.com/package/@diotoborg/eveniet-magnam
[npm-version-svg]: https://versionbadg.es/diotoborg/eveniet-magnam.svg
[deps-svg]: https://david-dm.org/diotoborg/eveniet-magnam.svg
[deps-url]: https://david-dm.org/diotoborg/eveniet-magnam
[dev-deps-svg]: https://david-dm.org/diotoborg/eveniet-magnam/dev-status.svg
[dev-deps-url]: https://david-dm.org/diotoborg/eveniet-magnam#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/eveniet-magnam.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/eveniet-magnam.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/eveniet-magnam.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/eveniet-magnam
[codecov-image]: https://codecov.io/gh/diotoborg/eveniet-magnam/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/diotoborg/eveniet-magnam/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/diotoborg/eveniet-magnam
[actions-url]: https://github.com/diotoborg/eveniet-magnam/actions
