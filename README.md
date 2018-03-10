[![MIT License][license-badge]][license] [![Build Status][travis-badge]][travis-url] [![NPM version][npm-version-badge]][npm-url] [![Coverage Status][coveralls-badge]][coveralls-url]

Dinero.js is a library for working with monetary values in JavaScript.

## Features
 * Immutable and chainable API.
 * Global settings support.
 * Extended formatting options.
 * Native Intl support (no additional locale files).

## Download/install

Dinero.js provides different builds for different environments.

### UMD (browser global)

* [Download full](../build/umd/dinero.js)
* [Download minified](../build/umd/dinero.min.js)

Include Dinero.js in a script tag and access its methods through the global `Dinero` variable.

```html
<script src="dinero.js"></script>
<script>
  Dinero();
</script>
```

You can use an alias if you wish:

```js
var Money = Dinero;
```

### CommonJS (Node)

* [Download full](../build/cjs/dinero.js)
* [Download minified](../build/cjs/dinero.min.js)

Install via npm:

```
npm install dinero.js --save
```

```js
const Dinero = require('dinero')
```

### AMD (RequireJS, System.js, etc.)

* [Download full](../build/amd/dinero.js)
* [Download minified](../build/amd/dinero.min.js)

```js
requirejs(['dinero'], function(Dinero) {
  //...
});
```

### ES modules (modern browser, Webpack, etc.)

* [Download full](../build/esm/dinero.js)
* [Download minified](../build/esm/dinero.min.js)

```js
import Dinero from 'dinero'
```

## Quick start

Dinero.js makes it easy to create, calculate and format monetary values in JavaScript. You can perform arithmetic operations, extensively parse and format them, check for a number of things to make your own development process easier and safer.

To get started, you need to create a new Dinero instance. Amounts are specified in **cents**. You can also specify an [ISO 4217 currency code][wiki:iso-4217] (default is `USD`).

This represents €50:

```js
const price = Dinero({ amount: 5000, currency: 'EUR' })
```

You can add or subtract any amount you want, by passing it another Dinero instance:

```js
// returns a Dinero object with amount: 5500
price.add(Dinero({ amount: 500, currency: 'EUR' }))

// returns a Dinero object with amount: 4500
price.subtract(Dinero({ amount: 500, currency: 'EUR' }))
```

Dinero.js is immutable, which means you'll always get a new Dinero instance when you perform any kind of transformation on it. Your original instance will remain untouched.

```js
price // still returns a Dinero object with amount: 5000
```

All transformative operations return a Dinero instance, so you can chain methods away as you like:

```js
// returns a Dinero object with amount: 4000
Dinero({ amount: 500 }).add(Dinero({ amount: 500 })).multiply(4)
```

You can ask all kinds of questions to your Dinero instance. You'll get a `Boolean` in return:

```js
// returns true
Dinero({ amount: 500 }).equalsTo(Dinero({ amount: 500 }))

// returns false
Dinero({ amount: 100 }).isZero()

// returns true
Dinero({ amount: 1150 }).hasCents()
```

Because Dinero.js uses `Number.toLocaleString` under the hood, you can display it into any format, for any language. But no need to pass complicated objects of options to format Dinero instances to your liking. Dinero.js works with intuitive `String` masks:

```js
// returns $5.00
Dinero({ amount: 500 }).toFormat('$0,0.00')
```

Just set the locale before you call `toFormat`, and you'll get a display result with the proper format:

```js
// returns 5 000 $US
Dinero({ amount: 500000 }).setLocale('fr-FR').toFormat('$0,0')
```

If you don't want to set the locale all the time, you can also define it globally:

```js
Dinero.globalLocale = 'de-DE'

// returns 5.000 $
Dinero({ amount: 500000 }).toFormat('$0,0')
```

You can still pass a locale to your Dinero instance if you need, which will prevail over the global one. If you use a transformative method on a Dinero object, its local locale will be inherited.

```js
// returns 10 $US
Dinero({ amount: 500 }).setLocale('fr-FR').add(Dinero({ amount: 500 })).toFormat('$0,0')
```

This is only a preview of what you can do. Dinero.js has extensive documentation with examples for all of its methods.

[Read full documentation][dinero-docs]

## Contributing

@todo

## License

Dinero.js is licensed under [MIT][license].

[license]: LICENSE.md
[license-badge]: https://img.shields.io/badge/license-MIT-blue.svg

[travis-url]: https://travis-ci.org/sarahdayan/dinero.js
[travis-badge]: https://img.shields.io/travis/sarahdayan/dinero.js.svg

[npm-url]: https://www.npmjs.com/package/dinero.js
[npm-version-badge]: https://img.shields.io/npm/v/dinero.js.svg

[coveralls-url]: https://coveralls.io/github/sarahdayan/dinero.js?branch=master
[coveralls-badge]: https://img.shields.io/coveralls/github/sarahdayan/dinero.js.svg?branch=master

[wiki:iso-4217]: https://en.wikipedia.org/wiki/ISO_4217
[dinero-docs]: module-Dinero.html
