# @stackline/vfile-find-up

> vfile utility to find one or more files by searching the file system upwards.

[![npm version](https://img.shields.io/npm/v/@stackline/vfile-find-up.svg?style=flat-square)](https://www.npmjs.com/package/@stackline/vfile-find-up)
[![license](https://img.shields.io/npm/l/@stackline/vfile-find-up.svg?style=flat-square)](https://github.com/alexandroit/stackline-vfile-find-up)
[![GitHub repository](https://img.shields.io/badge/GitHub-alexandroit%2Fstackline-vfile-find-up-181717?style=flat-square&logo=github)](https://github.com/alexandroit/stackline-vfile-find-up)
[![Docs](https://img.shields.io/badge/docs-alexandro.net-0f766e?style=flat-square)](https://alexandro.net/docs/vanilla/vfile-find-up/)
[![Reddit community](https://img.shields.io/badge/community-r%2FStackline-ff4500?style=flat-square&logo=reddit&logoColor=white)](https://www.reddit.com/r/Stackline/)

**[Documentation](https://alexandro.net/docs/vanilla/vfile-find-up/)** | **[npm](https://www.npmjs.com/package/@stackline/vfile-find-up)** | **[Issues](https://github.com/alexandroit/stackline-vfile-find-up/issues)** | **[Repository](https://github.com/alexandroit/stackline-vfile-find-up)**

**Current package version:** `1.0.1`

---

## Why this package?

`@stackline/vfile-find-up` is the Stackline-maintained distribution of `vfile-find-up@6.1.0`. It is an independent continuation of [vfile-find-up](https://github.com/vfile/vfile-find-up); original authors and licenses remain credited below.

## Compatibility

| Item | Value |
| :--- | :--- |
| Package | `@stackline/vfile-find-up@1.0.1` |
| API target | `vfile-find-up@6.1.0` |
| Supported Node.js | `See supported framework requirements` |
| License | `MIT` |
| Module type | `module` |
| Main entry | `index.js` |
| Types | `index.d.ts` |
| Runtime dependencies | `vfile, to-vfile` |

## Installation

```bash
npm install @stackline/vfile-find-up
```

Preserve existing imports and plugin resolution with an npm alias:

```bash
npm install vfile-find-up@npm:@stackline/vfile-find-up
```

## Usage and API reference

### vfile-find-up


[vfile][] utility to find files by searching the file system upwards.

## Contents

*   [What is this?](#what-is-this)
*   [When should I use this?](#when-should-i-use-this)
*   [Install](#install)
*   [Use](#use)
*   [API](#api)
    *   [`findUp(tests[, path][, callback])`](#finduptests-path-callback)
    *   [`findUpOne(test[, path][, callback])`](#finduponetest-path-callback)
    *   [`BREAK`](#break)
    *   [`INCLUDE`](#include)
    *   [`Assert`](#assert)
    *   [`Callback`](#callback)
    *   [`CallbackOne`](#callbackone)
    *   [`Test`](#test)
*   [Types](#types)
*   [Compatibility](#compatibility)
*   [Contribute](#contribute)
*   [License](#license)

## What is this?

This utility lets you find one or many files upwards.

## When should I use this?

You can use this utility if you want to find, say, a config file.
If you instead want to find files downwards, such as all markdown files in a
folder, you can use [`vfile-find-down`][vfile-find-down].

## Install

This package is [ESM only][esm].
In Node.js (version 14.14+ and 16.0+), install with [npm][]:

```sh
npm install @stackline/vfile-find-up
```

## Use

```js
import {findUp} from '@stackline/vfile-find-up'

console.log(await findUp('package.json'))
```

Yields:

```js
[ VFile {
  data: {},
  messages: [],
  history: [ '/Users/tilde/projects/oss/vfile-find-up/package.json' ],
  cwd: '/Users/tilde/projects/oss/vfile-find-up' } ]
```

## API

This package exports the identifiers
[`BREAK`][api-break],
[`INCLUDE`][api-include],
[`findUp`][api-find-up], and
[`findUpOne`][api-find-up-one].
There is no default export.

### `findUp(tests[, path][, callback])`

Find files or folders upwards.

> 👉 **Note**: files are not read (their `value` is not populated).

###### Signatures

*   `(test[, path], callback) => void`
*   `(test[, path]) => Promise<Array<VFile>>`

###### Parameters

*   `test` ([`Test`][api-test])
    — things to search for
*   `paths` (`string`, default: `process.cwd()`)
    — place to search from
*   `callback` ([`Callback`][api-callback], optional)
    — callback called when done

###### Returns

Nothing when `callback` is given (`void`), otherwise a promise that resolves to
files ([`Array<VFile>`][vfile]).

### `findUpOne(test[, path][, callback])`

Find the first file or folder upwards.

> 👉 **Note**: files are not read (their `value` is not populated).

###### Signatures

*   `(test[, path], callback) => void`
*   `(test[, path]) => Promise<VFile>`

###### Parameters

*   `test` ([`Test`][api-test])
    — things to search for
*   `path` (`string`, default: `process.cwd()`)
    — place to search from
*   `callback` ([`CallbackOne`][api-callback-one], optional)
    — callback called when done

###### Returns

Nothing when `callback` is given (`void`), otherwise a promise that resolves to
a file ([`VFile | null`][vfile]).

### `BREAK`

Stop searching (`number`).

### `INCLUDE`

Include this file (`number`).

### `Assert`

Handle a file (TypeScript type).

###### Parameters

*   `file` ([`VFile`][vfile])
    — file to handle

###### Returns

How to handle this file (`boolean | number`, optional).

`true` is treated as `INCLUDE`.

### `Callback`

Callback called when done (TypeScript type).

###### Parameters

*   `error` (`Error | null`)
    — error; errors are currently never passed
*   `files` ([`Array<VFile>`][vfile])
    — files

###### Returns

Nothing (`void`).

### `CallbackOne`

Callback called when done finding one file (TypeScript type).

###### Parameters

*   `error` (`Error | null`)
    — error; errors are currently never passed
*   `file` ([`VFile | null`][vfile])
    — file

###### Returns

Nothing (`void`).

### `Test`

Things to search for (TypeScript type).

For strings, the `basename` or `extname` of files must match them.
For arrays, any test in them must match.

###### Type

```ts
type Test = Array<Assert | string> | Assert | string
```

## Types

This package is fully typed with [TypeScript][].
It exports the additional types
[`Assert`][api-assert],
[`Callback`][api-callback],
[`CallbackOne`][api-callback-one], and
[`Test`][api-test].

## Compatibility

Projects maintained by the unified collective are compatible with all maintained
versions of Node.js.
As of now, that is Node.js 14.14+ and 16.0+.
Our projects sometimes work with older versions, but this is not guaranteed.

## Contribute

See [`contributing.md`][contributing] in [`vfile/.github`][health] for ways to
get started.
See [`support.md`][support] for ways to get help.

This project has a [code of conduct][coc].
By interacting with this repository, organization, or community you agree to
abide by its terms.

## License

[MIT][license] © [Titus Wormer][author]



[build-badge]: https://github.com/vfile/vfile-find-up/workflows/main/badge.svg

[build]: https://github.com/vfile/vfile-find-up/actions

[coverage-badge]: https://img.shields.io/codecov/c/github/vfile/vfile-find-up.svg

[coverage]: https://codecov.io/github/vfile/vfile-find-up

[downloads-badge]: https://img.shields.io/npm/dm/vfile-find-up.svg

[downloads]: https://www.npmjs.com/package/vfile-find-up

[sponsors-badge]: https://opencollective.com/unified/sponsors/badge.svg

[backers-badge]: https://opencollective.com/unified/backers/badge.svg

[collective]: https://opencollective.com/unified

[chat-badge]: https://img.shields.io/badge/chat-discussions-success.svg

[chat]: https://github.com/vfile/vfile/discussions

[npm]: https://docs.npmjs.com/cli/install

[esm]: https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c

[typescript]: https://www.typescriptlang.org

[contributing]: https://github.com/vfile/.github/blob/main/contributing.md

[support]: https://github.com/vfile/.github/blob/main/support.md

[health]: https://github.com/vfile/.github

[coc]: https://github.com/vfile/.github/blob/main/code-of-conduct.md

[license]: license

[author]: https://wooorm.com

[vfile]: https://github.com/vfile/vfile

[vfile-find-down]: https://github.com/vfile/vfile-find-down

[api-break]: #break

[api-include]: #include

[api-find-up]: #finduptests-path-callback

[api-find-up-one]: #finduponetest-path-callback

[api-assert]: #assert

[api-callback]: #callback

[api-callback-one]: #callbackone

[api-test]: #test

## Credits and original authors

- Original project: [vfile-find-up](https://github.com/vfile/vfile-find-up).
- Titus Wormer.
- Copyright (c) 2015 Titus Wormer <tituswormer@gmail.com>.
- Stackline maintenance: [Alexandro Paixao Marques](https://www.linkedin.com/in/aleinfo/) and [Stackline contributors](https://github.com/alexandroit).

Original copyright, license notices and contributor acknowledgements remain part of this distribution. Stackline maintenance does not replace authorship of the original work.

## Community and Links

- [Stackline website](https://alexandro.net/)
- [GitHub projects](https://github.com/alexandroit)
- [npm packages](https://www.npmjs.com/~alex360qc)
- [Reddit community — r/Stackline](https://www.reddit.com/r/Stackline/)
- [Maintainer LinkedIn](https://www.linkedin.com/in/aleinfo/)

Use this repository's issue tracker for reproducible bugs and feature requests. Join r/Stackline for examples, usage questions and release discussions.
