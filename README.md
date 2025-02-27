# OpenCV-Contrib-Wasm
*(This is a fork of [OpenCV-Wasm](https://github.com/echamudi/opencv-wasm) with the added opencv_contrib modules) Unless you are using a module like aruco, you will want to the original repo this was forked from.*

[![Test](https://github.com/Hpmason/opencv-contrib-wasm/actions/workflows/test.yml/badge.svg)](https://github.com/Hpmason/opencv-contrib-wasm/actions/workflows/test.yml)

Precompiled OpenCV to JavaScript + WebAssembly for node.js and deno environment. 🦕

In this Wasm-compiled OpenCV, there's no need to have OpenCV installed in the machine. The entire OpenCV library is already inside this package (`opencv.js` and `opencv.wasm`).

This module has zero dependencies.

## Examples

| Code | Input | Output |
|---|---|---|
| [dilation.js](./examples/dilation.js) (node) [dilation.ts](./examples/deno/dilation.ts) (deno)| ![image sample 1](./examples/input/image-sample-1.jpg) | ![dilation](./examples/expected-output/dilation.png) |
| [templateMatching.js](./examples/templateMatching.js) (node) [templateMatching.ts](./examples/deno/templateMatching.ts) (deno)| source:<br>![image sample 2](./examples/input/image-sample-2.png) <br>template:<br> ![image sample 2 template](./examples/input/image-sample-2-template.png) | ![template matching](./examples/expected-output/template-matching.png) |

## Installation

### node

```
npm install @hpmason/opencv-contrib-wasm
```
Code example:
```js
const { cv, cvTranslateError } = require('@hpmason/opencv-contrib-wasm');

let mat = cv.matFromArray(2, 3, cv.CV_8UC1, [1, 2, 3, 4, 5, 6]);
console.log('cols =', mat.cols, '; rows =', mat.rows);
console.log(mat.data8S);

cv.transpose(mat, mat);
console.log('cols =', mat.cols, '; rows =', mat.rows);
console.log(mat.data8S);

/*
cols = 3 ; rows = 2
Int8Array(6) [ 1, 2, 3, 4, 5, 6 ]
cols = 2 ; rows = 3
Int8Array(6) [ 1, 4, 2, 5, 3, 6 ]
*/
```

### deno

```ts
import { cv, cvTranslateError } from 'https://deno.land/x/opencv_contrib@v4.5.3-0/mod.ts';
// Change the @<version> with the latest or any version you desire.
// Check the available versions here: https://deno.land/x/opencv_contrib.
```
Code example:
```ts
import { cv, cvTranslateError } from 'https://deno.land/x/opencv_contrib@v4.5.3-0/mod.ts';

let mat = cv.matFromArray(2, 3, cv.CV_8UC1, [1, 2, 3, 4, 5, 6]);
console.log('cols =', mat.cols, '; rows =', mat.rows);
console.log(mat.data8S);

cv.transpose(mat, mat);
console.log('cols =', mat.cols, '; rows =', mat.rows);
console.log(mat.data8S);

/*
cols = 3 ; rows = 2
Int8Array(6) [ 1, 2, 3, 4, 5, 6 ]
cols = 2 ; rows = 3
Int8Array(6) [ 1, 4, 2, 5, 3, 6 ]
*/
```

## Usage

Because this module is using the same code as the official OpenCV.js for the web, you can use the same documentation at the web: https://docs.opencv.org/4.5.3/d5/d10/tutorial_js_root.html

There are some minor initialization changes, because this module will be loaded synchronously instead of the OpenCV's default (asynchronously). 

You can check the files inside [examples](./examples) folder as reference on how to initialize, loading images, and saving images.

## Error Handling

By default, mistakes in code will produce error code. You can use the following snippet to translate the error code into meaningful statement from OpenCV.

```js
const { cv, cvTranslateError } = require('@hpmason/opencv-contrib-wasm');

try {
    // Your OpenCV code
} catch (err) {
    console.log(cvTranslateError(cv, err));
}
```

## Versioning

This npm module uses the following versioning number:
```
<opencv version>-<this module version>
```
For Example
```
4.5.3-0
OpenCV version 4.5.3
OpenCV-Contrib-Wasm Module version 0
```

## Development

### Building

Run the following script on macOS or Linux (tested on Ubuntu). You need docker on the system.

```
npm install
(cd ./utils && sh ./build.sh)
(cd utils && node generateCvProps.js)
```

### Testing

After completing the build script, you can run the test provided by OpenCV, and the test from this repo.

```sh
# OpenCV's test
(cd ./build_wasm_test/bin && npm install)
(cd ./build_wasm_test/bin && node tests.js)

# This repo's test
npm test
```

## Authors

* **Ezzat Chamudi** (Original work and repo) - [echamudi](https://github.com/echamudi)
* **Mason Ginter** (This fork) - [hpmason](https://github.com/hpmason)

See also the list of [contributors](https://github.com/hpmason/opencv-contrib-wasm/graphs/contributors) who participated in this project.

## License

Copyright © 2020 [Ezzat Chamudi](https://github.com/echamudi), [Mason Ginter](https://github.com/echamudi), and [OpenCV-Wasm Project Authors](https://github.com/hpmason/opencv-contrib-wasm/graphs/contributors)

OpenCV-Contrib-Wasm code is licensed under [BSD-3-Clause](https://opensource.org/licenses/BSD-3-Clause). Images, logos, docs, and articles in this project are released under [CC-BY-SA-4.0](https://creativecommons.org/licenses/by-sa/4.0/legalcode).

[OpenCV License](https://opencv.org/license/).

Libraries, dependencies, and tools used in this project are tied with their licenses.
