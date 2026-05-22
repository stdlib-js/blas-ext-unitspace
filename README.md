<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# unitspace

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Return a new [ndarray][@stdlib/ndarray/ctor] filled with linearly spaced numeric elements which increment by `1` starting from a specified value along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.



<section class="usage">

## Usage

To use in Observable,

```javascript
unitspace = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-unitspace@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var unitspace = require( 'path/to/vendor/umd/blas-ext-unitspace/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-unitspace@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.unitspace;
})();
</script>
```

#### unitspace( shape, start\[, options] )

Returns a new [ndarray][@stdlib/ndarray/ctor] filled with linearly spaced numeric elements which increment by `1` starting from a specified value along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
var x = unitspace( [ 4 ], 1.0 );
// returns <ndarray>[ 1.0, 2.0, 3.0, 4.0 ]
```

The function has the following parameters:

-   **shape**: array shape.
-   **start**: starting value. May be either a number, a complex number, or an [ndarray][@stdlib/ndarray/ctor] having a numeric or "generic" [data type][@stdlib/ndarray/dtypes]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, a start [ndarray][@stdlib/ndarray/ctor] must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input shape, a start [ndarray][@stdlib/ndarray/ctor] must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function generates linearly spaced values along the last dimension. Default: `[-1]`.
-   **dtype**: output [ndarray][@stdlib/ndarray/ctor] [data type][@stdlib/ndarray/dtypes]. Must be a numeric or "generic" [data type][@stdlib/ndarray/dtypes]. If a data type is provided, `start` is cast to the specified data type. If a data type is not provided, the default output array data type is the same as the data type of `start`.
-   **order**: specifies whether an [ndarray][@stdlib/ndarray/ctor] is `'row-major'` (C-style) or `'column-major'` (Fortran-style). If `start` is a scalar value, the default order is `'row-major'`. If `start` is an [ndarray][@stdlib/ndarray/ctor], the default order is the same as the memory layout of `start`.
-   **mode**: specifies how to handle indices which exceed array dimensions (see [`ndarray`][@stdlib/ndarray/ctor]). Default: `'throw'`.
-   **submode**: a mode array which specifies for each dimension how to handle subscripts which exceed array dimensions (see [`ndarray`][@stdlib/ndarray/ctor]). If provided fewer modes than dimensions, the function recycles modes using modulo arithmetic. Default: `[ options.mode ]`.

When provided a scalar or zero-dimensional [ndarray][@stdlib/ndarray/ctor] `start` argument, the value is broadcast across all elements in the shape defined by the complement of those dimensions specified by `options.dims`. To specify separate sub-array starting values, provide a non-zero-dimensional [ndarray][@stdlib/ndarray/ctor] argument.

```javascript
var array = require( '@stdlib/ndarray-array' );

var start = array( [ 1.0, 5.0 ] );
// returns <ndarray>[ 1.0, 5.0 ]

var x = unitspace( [ 2, 3 ], start );
// returns <ndarray>[ [ 1.0, 2.0, 3.0 ], [ 5.0, 6.0, 7.0 ] ]
```

By default, the function generates linearly spaced values along the last dimension of an output [ndarray][@stdlib/ndarray/ctor]. To perform the operation over specific dimensions, provide a `dims` option.

```javascript
var x = unitspace( [ 2, 2 ], 1.0, {
    'dims': [ 0, 1 ]
});
// returns <ndarray>[ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ]
```

To specify the output [ndarray][@stdlib/ndarray/ctor] [data type][@stdlib/ndarray/dtypes], provide a `dtype` option.

```javascript
var x = unitspace( [ 4 ], 1.0, {
    'dtype': 'float32'
});
// returns <ndarray>[ 1.0, 2.0, 3.0, 4.0 ]
```

#### unitspace.assign( x, start\[, options] )

Fills an [ndarray][@stdlib/ndarray/ctor] with linearly spaced numeric elements which increment by `1` starting from a specified value along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
var zeros = require( '@stdlib/ndarray-zeros' );

var x = zeros( [ 4 ] );
// returns <ndarray>[ 0.0, 0.0, 0.0, 0.0 ]

var out = unitspace.assign( x, 1.0 );
// returns <ndarray>[ 1.0, 2.0, 3.0, 4.0 ]

var bool = ( x === out );
// returns true
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a numeric or "generic" [data type][@stdlib/ndarray/dtypes].
-   **start**: starting value. May be either a number, a complex number, or an [ndarray][@stdlib/ndarray/ctor] having a numeric or "generic" [data type][@stdlib/ndarray/dtypes]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, a start [ndarray][@stdlib/ndarray/ctor] must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], a start [ndarray][@stdlib/ndarray/ctor] must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function generates linearly spaced values along the last dimension. Default: `[-1]`.

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   When writing to a complex floating-point output [ndarray][@stdlib/ndarray/ctor], a real-valued `start` value is treated as a complex number having a real component equaling the provided value and having an imaginary component equaling zero.
-   The `start` argument is cast to the data type of the output [ndarray][@stdlib/ndarray/ctor].
-   The function iterates over [ndarray][@stdlib/ndarray/ctor] elements according to the memory layout of an output [ndarray][@stdlib/ndarray/ctor]. Accordingly, performance degradation is possible when operating over multiple dimensions of a large non-contiguous multi-dimensional output [ndarray][@stdlib/ndarray/ctor]. In such scenarios, one may want to copy an output [ndarray][@stdlib/ndarray/ctor] to contiguous memory before filling with linearly spaced values.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-unitspace@umd/browser.js"></script>
<script type="text/javascript">
(function () {

// Create a vector of starting values:
var start = unitspace( [ 5 ], 1 );

// Create a grid:
var out = unitspace( [ 5, 5 ], start );
console.log( ndarray2array( out ) );

// Generate values over multiple dimensions:
out = unitspace( [ 5, 5 ], 1, {
    'dims': [ 0, 1 ]
});
console.log( ndarray2array( out ) );

// Generate values over multiple dimensions in column-major order:
out = unitspace( [ 5, 5 ], 1, {
    'dims': [ 0, 1 ],
    'order': 'column-major'
});
console.log( ndarray2array( out ) );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-unitspace.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-unitspace

[test-image]: https://github.com/stdlib-js/blas-ext-unitspace/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/blas-ext-unitspace/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-unitspace/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-unitspace?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-unitspace.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-unitspace/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-unitspace/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-unitspace/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-unitspace/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-unitspace/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-unitspace/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-unitspace/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-unitspace/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-unitspace/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/umd

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/umd

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes/tree/umd

</section>

<!-- /.links -->
