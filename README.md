[![Build Status](https://travis-ci.org/pelevesque/has-required-substrings-at-indexes.svg?branch=master)](https://travis-ci.org/pelevesque/has-required-substrings-at-indexes)
[![Coverage Status](https://coveralls.io/repos/github/pelevesque/has-required-substrings-at-indexes/badge.svg?branch=master)](https://coveralls.io/github/pelevesque/has-required-substrings-at-indexes?branch=master)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

# has-required-substrings-at-indexes

Checks if a string has required substrings at given indexes.

## Related Packages

https://github.com/pelevesque/has_required_substrings  
https://github.com/pelevesque/has_required_substrings_after_sums  
https://github.com/pelevesque/has_prohibited_substring  
https://github.com/pelevesque/has_prohibited_substring_at_indexes  
https://github.com/pelevesque/has_prohibited_substring_after_sums  

## Node Repository

https://www.npmjs.com/package/@pelevesque/has-required-substrings-at-indexes

## Installation

`npm install @pelevesque/has-required-substrings-at-indexes`

## Tests

Command                      | Description
---------------------------- | ------------
`npm test` or `npm run test` | All Tests Below
`npm run cover`              | Standard Style
`npm run standard`           | Coverage
`npm run unit`               | Unit Tests

## Usage

### Parameters

```js
str                (required)
requiredSubstrings (required)
options            (optional) default = { allowLastSubstringToBleed = false, ignoreSubstringsOutsideString = false }
```

### Requiring

```js
const hasRequiredSubstringsAtIndexes = require('@pelevesque/has-required-substrings-at-indexes')
```

### Basic Usage

`requiredSubstrings` is an object of index -> substring pairs. `true` is returned
if all substrings are found at the correct indexes.

```js
const str = 'abcde'
const requiredSubstrings = { 0: 'f' }
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings)
// result === false
```

```js
const str = 'abcde'
const requiredSubstrings = { 5: 'f' }
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings)
// result === false
```

```js
const str = 'abcde'
const requiredSubstrings = { 0: 'a', 2: 'c', 4: 'a' }
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings)
// result === false
```

```js
const str = 'abcde'
const requiredSubstrings = { 0: 'a', 2: 'c', 4: 'e' }
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings)
// result === true
```

```js
const str = 'a man a plan a canal'
const requiredSubstrings = { 2: 'man', 8: 'plan', 15: 'canal' }
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings)
// result === true
```

### Options

#### allowLastSubstringToBleed

The `allowLastSubstringToBleed` option is `false` by default. It it used when you want
to allow the last substring to be incomplete if the string is too short.
In the following example, the last substring `canal` starts at the correct index,
but remains incomplete since the string ends. Normally this would return `false`.
With `allowLastSubstringToBleed` set to `true`, it returns `true`.

```js
const str = 'a man a plan a c'
const requiredSubstrings = { 2: 'man', 8: 'plan', 15: 'canal' }
const allowLastSubstringToBleed = true
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings, {
  allowLastSubstringToBleed: allowLastSubstringToBleed
})
// result === true
```

#### ignoreIndexesOutsideString

The `ignoreIndexesOutsideString` option is `false` by default. When set to `true`,
required substring indexes that fall outside the string length will be ignored.

```js
const str = 'abcde'
const requiredSubstrings = { 5: 'f' }
const ignoreIndexesOutsideString = true
const result = hasRequiredSubstringsAtIndexes(str, requiredSubstrings, {
  ignoreIndexesOutsideString: ignoreIndexesOutsideString
})
// result === true
```
