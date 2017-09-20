# metalsmith-postcss

[![Greenkeeper badge](https://badges.greenkeeper.io/axa-ch/metalsmith-postcss.svg)](https://greenkeeper.io/)

[![Build Status](https://travis-ci.org/axa-ch/metalsmith-postcss.svg?branch=master)](https://travis-ci.org/axa-ch/metalsmith-postcss)

> A Metalsmith plugin that sends your CSS
> through any [PostCSS](https://github.com/postcss/postcss) plugins.

## Installation

```sh
npm install metalsmith-postcss
```

## Getting Started

If you haven't checked out [Metalsmith](http://metalsmith.io/) before,
head over to their website and check out the documentation.

## JavaScript API

Using the JavaScript api for Metalsmith,
just add the postcss package name, optionally with it’s
options, to your `.use()` directives. Here is an example
using `postcss-pseudoelements` and `postcss-nested` to
transform your source files.

```js
var postcss = require('metalsmith-postcss');

metalsmith.use(postcss({
  plugins: {
    'postcss-pseudoelements': {}
    'postcss-nested': {}
  }
}));
```

## Metalsmith CLI

Using the Metalsmith CLI, just add the postcss package name,
optionally with it’s options, to your `metalsmith.json` config.
Here is an example using `postcss-pseudoelements` and `postcss-nested`
to transform your source files.

```js
"metalsmith-postcss": {
  "plugins": {
    "postcss-pseudoelements": {},
    "postcss-nested": {}
  },
  "map": true
}
```

## Alternative plugin definition syntax

Sometime in PostCSS, plugins need to be defined in a certain order and JavaScript
Objects cannot guarantee the order of keys in an object. Therefore, you are able
to specify PostCSS plugins using an array of objects(which can guarantee the order
  of loading).

```js
"metalsmith-postcss": {
  "plugins": [
    "postcss-pseudoelements",
    {
      "postcss-nested": {
        "some": "config"
      }
    }
  ]
}
```

## Sourcemaps

This plugin doesn't generate sourcemaps by default. However, you
can enable them using several ways.

### Inline sourcemaps

Add `map: true` to the `options` argument to get your
sourcemaps written into the source file.

```js
metalsmith.use(postcss({
  plugins: {},
  map: true
}));
```

Behind the scenes, this resolves to the following:

```js
metalsmith.use(postcss({
  plugins: {},
  map: {
    inline: true
  }
}));
```

### External sourcemaps

If you don't want to have your files polluted with sourcemaps,
just set `inline: false`. Using that, you'll get `.map` files
generated beside your sources.

```js
metalsmith.use(postcss({
  plugins: {},
  map: {
    inline: false
  }
}));
```

## Test

To run the tests use:

```sh
npm test
```
