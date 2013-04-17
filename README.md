# rsz [![Build Status](https://secure.travis-ci.org/rvagg/node-rsz.png)](http://travis-ci.org/rvagg/node-rsz)

**Resize image files or `Buffer`s**

Depends on [node-canvas](https://github.com/LearnBoost/node-canvas) which has special [build instructions](https://github.com/LearnBoost/node-canvas/wiki/_pages) as it requires **Cairo** to be installed on your system.

## Related

**rsz** shares the same API as **[crp](https://github.com/rvagg/node-crp)**, except **crp** is for *cropping* images rather than resizing. See also **[sz](https://github.com/rvagg/node-sz)** for simply obtaining the *size* of an image.

## API

There is one method but multiple ways to use it:

<b>rsz(src, width, height, function (err, buf) { /* */ })</b>

Where <b><code>src</code></b> is a `String` specifying the path to the image or a `Buffer` containing the image data, and <b><code>buf</code></b> is a `Buffer` containing the resized image data.

<b>rsz(src, width, height, dst, function (err) { /* */ })</b>

Where <b><code>src</code></b> is a `String` specifying the path to the image or a `Buffer` containing the image data, and <b><code>dst</code></b> is a `String` specifying the path to write the output file to.

<b>rsz(src, { width: w, height: h }, function (err, buf) { /* */ })</b>

Where <b><code>w</code></b> and <b><code>h</code></b> are the width and height respectively, <b><code>src</code></b> is a `String` specifying the path to the image or a `Buffer` containing the image data, and <b><code>buf</code></b> is a `Buffer` containing the resized image data.

<b>rsz(src, { width: w, height: h }, dst, function (err) { /* */ })</b>

Where <b><code>w</code></b> and <b><code>h</code></b> are the width and height respectively, <b><code>src</code></b> is a `String` specifying the path to the image or a `Buffer` containing the image data, and <b><code>dst</code></b> is a `String` specifying the path to write the output file to.

## Options

By default, **rsz** will return a **PNG** `Buffer` or write a **PNG** file. You can change this when you pass an `options` object: `{ height: 100, width: 100, type: 'jpeg' }`. You can also adjust the quality with a `'quality'` property.

 * <b><code>'height'</code></b> (`Number`, required) the height of the resized image
 * <b><code>'width'</code></b> (`Number`, required) the width of the resized image
 * <b><code>'type'</code></b> (`String`, optional, default: `'png'`) set to `'jpeg'` to return a **JPEG** `Buffer` or write a **JPEG** file.
 * <b><code>'quality'</code></b> (`Number`, optional) used when creating a **JPEG**, a number between 1 (lowest quality) and 100 (highest quality).

## Example

```js
var rsz = require('rsz')
  , fs  = require('fs')

rsz('/path/to/nyancat.gif', 200, 350, function (err, buf) {
  fs.writeFileSync('/path/to/nyancat_200_350.png', buf)
})

// or

rsz('/path/to/nyancat.gif', 200, 350, '/path/to/nyancat_200_350.png', function (err) {
})

// or

rsz('/path/to/nyancat.gif', { width: 200, height: 350 }, function (err, buf) {
  fs.writeFileSync('/path/to/nyancat_200_350.png', buf)
})

// or

rsz('/path/to/nyancat.gif', { width: 200, height: 350 }, '/path/to/nyancat_200_350.png', function (err) {
})

// or a jpeg

rsz(
    '/path/to/avatar.png'
  , { width: 50, height: 50, type: 'jpeg', quality: 40 }
  , '/path/to/avatar_50_50.jpg'
  , function (err) {
      /* ... */
    }
)
```

## Licence

rsz is Copyright (c) 2013 Rod Vagg [@rvagg](https://twitter.com/rvagg) and licensed under the MIT licence. All rights not explicitly granted in the MIT license are reserved. See the included LICENSE file for more details.