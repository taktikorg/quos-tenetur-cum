# @taktikorg/quos-tenetur-cum <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Define an accessor property on an object. In an engine without descriptors, in loose mode, when only a getter is provided, nonEnumerable is false, and nonConfigurable is false, wil fall back to assignment - otherwise, it will throw.

The two `non*` options can also be passed `null`, which will use the existing state if available.

The `loose` option will mean that if you attempt to set a nonconfigurable/nonwritable accessor property with `set`, in an environment without descriptor support, it will fall back to normal assignment (and eagerly evaluate the getter).

## Usage

```javascript
var defineAccessorProperty = require('@taktikorg/quos-tenetur-cum');
var assert = require('assert');

var str = 'value';
var strThunk = function () { return str; };
var strSetter = function (v) { str = v; };
var random = function () { return Math.random(); };

var obj = {};
defineAccessorProperty(
	obj,
	'key',
	{
		get: strThunk,
		set: strSetter,
	}
);
defineAccessorProperty(
	obj,
	'key2',
	{
		get: random, // at least one of "get" or "set" must be provided
		nonConfigurable: true, // optional
		nonEnumerable: true, // optional
		loose: false, // optional
	}
);

assert.deepEqual(
	Object.getOwnPropertyDescriptors(obj),
	{
		key: {
			configurable: true,
			enumerable: true,
			get: strThunk,
			set: strSetter,
		},
		key2: {
			configurable: false,
			enumerable: false,
			get: random,
			set: undefined,
		},
	}
);
```

[package-url]: https://npmjs.org/package/@taktikorg/quos-tenetur-cum
[npm-version-svg]: https://versionbadg.es/ljharb/@taktikorg/quos-tenetur-cum.svg
[deps-svg]: https://david-dm.org/ljharb/@taktikorg/quos-tenetur-cum.svg
[deps-url]: https://david-dm.org/ljharb/@taktikorg/quos-tenetur-cum
[dev-deps-svg]: https://david-dm.org/ljharb/@taktikorg/quos-tenetur-cum/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@taktikorg/quos-tenetur-cum#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@taktikorg/quos-tenetur-cum.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@taktikorg/quos-tenetur-cum.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@taktikorg/quos-tenetur-cum.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@taktikorg/quos-tenetur-cum
[codecov-image]: https://codecov.io/gh/ljharb/@taktikorg/quos-tenetur-cum/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@taktikorg/quos-tenetur-cum/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@taktikorg/quos-tenetur-cum
[actions-url]: https://github.com/taktikorg/quos-tenetur-cum/actions
