# path.parse() from Node.js without unnecessary semver bumps

See [packaged-path-parse](https://github.com/ChALkeR/packaged-path-parse) for
documentation, this module just is a re-export of that without unnecessary
major- and minor- version bumps.

## Why?

[packaged-path-parse](https://github.com/ChALkeR/packaged-path-parse) and
`compatible-path-parse` were designed to come in pair.

`packaged-path-parse` packages
[path.parse()](https://nodejs.org/api/path.html#path_path_parse_path) from a
recent Node.js version under the same version as Node.js that the code
originated from — to provide clear understanding of the Node.js version used as
the source, to ease updating this module, and to give predictable behavior.

Because of that while `packaged-path-parse` conforms to semver requirements,
it bumps versions more often than it should be done (but no needed bumps are
missed).

So, this package provides additional semver goodness on top of that, making sure
that `minor-` and `major-` versions of this package is not bumped when that is
not needed by `path.parse()` implementation.

I.e. `minor-` versions of `packaged-path-parse` that do not actually bring any
any additions (where a Node.js version bump was caused was caused by something
other than `path.parse()`) will be included in a `patch-` release of this
package. The same for `major-` versions of `packaged-path-parse` that do
not bring any incompatibilities (and were just inherited from Node.js) — those
will be either a `minor-` or a `patch-` versions of this package.

That said, this package conforms to semver and any imcompatible changes in
`packaged-path-parse` will bump the `major-` version, and new additions will
bump the `minor-` version.

**That way you, and your users will get important updates faster, and that will
better de-duplicate the code in case of several packages using this one.**

## Ponyfill

This module fits all definitions of being a [ponyfill](https://ponyfill.com).

## Usage

See [path.parse()](https://nodejs.org/api/path.html#path_path_parse_path)
documentation.

```js
const pathParse = require('compatible-path-parse')
pathParse(path) // platform-dependant, default — posix
pathParse.posix(path) // posix
pathParse.win32(path) // win32
```

## License

MIT. See `LICENSE` file.
