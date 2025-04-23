# Changelog
This file based on a [Keep a Changelog](http://keepachangelog.com/en/1.0.0/) agreement.

## 0.16.0 - 21-05-20
### Added
  - `kebabCase` function added

## 0.15.1 - 14-05-20
### Changed
  - Replaced a jest report on `jest-html-reporters`

## 0.15.0 - 06-05-20
### Added
  - `truncate` function added

## 0.14.0 - 24-04-20
### Added
  - `upperFirst` function added

## 0.13.0 - 17-04-20
### Added
  - `clamp` function added

## 0.12.0 - 13-04-20
### Added
  - `lowerFirst` function added

## 0.11.3 - 02-04-20
  - `template` functions in data render are permissive in arguments but more strict in return type

## 0.11.2 - 01-04-20
  - `template` options argument (data for render) now also accepts functions

## 0.11.1 - 01-04-20
  - `template` options argument (data for render) now accepts all primitives, not only `string | number`

## 0.11.0 - 25-03-20
  - `template` function added

## 0.10.0 - 22-03-20
  - `pick` now accepts string tuples as well as `string[]`
  - `keyBy` does not add `void` to collection values

## 0.9.0 - 29-08-19
  - `MergeLeft` renamed to `MergeRight`
  - `prop` is simplified and checks keys only

## 0.8.2 - 15-08-19

### Added
  - `intersection` function

## 0.8.1 - 08-06-19

### Fixed
  - veendor suffix

### Added
  - `capitalize` function

## 0.8.0 - 08-05-19
### Fixed
  - `any` takes $ReadOnlyArray<T> instead of Array<T>

### Added
  - `split` and `join` functions

## 0.7.1 - 05-04-19
### Fixed
  - `identity` casted to any before casting to proper type (flow 0.6x error)

## 0.7.0 - 01-04-19
### Added
  - `take` and `takeRight` functions
  - `differenceWith` function
  - `flatten` function
  - `noop` function

### Changed
  - `constant` and `identity` functions support multiple arguments
  - `index.js` with list of functions now follow alphabetical order

## 0.6.1 - 23-03-19
### Added
  - `times` function

## 0.6.0 - 19-03-19
### Added
  - `headOr` function
  - `tailOr` function

### Fixed
  - `tail` now resolves rare case of empty tuple as `empty`

## 0.5.0 - 19-03-19
### Fixed
  - Object with `{length: 0}` now is not considered by the isEmpty function as `true` (more soundness!)

### Changed
  - `head` and `headOrIdentity` now resolves rare case of empty tuple as `empty`

## 0.4.3 - 15-03-19
### Fixed
  - pathOrUnsafe now more tolerant to nullable source (as it should be)
  - pathOrUnsafe now accepts $ReadOnlyArrays with keys

## 0.4.2 - 11-03-19
### Added
  - `snakeCase` function
### Fixed
  - Documentation build command fixed

## 0.4.1 - 10-02-19
### Fixed
  - Wrong `prop` key generic

## 0.4.0 - 03-02-19
### Added
 - New `isEqual` and `isEqualUnsafe` functions
 - New `remove` function (opposite of `filter`)
 - New `has` function with `Object.hasOwnProperty` semantics
 - Some typos fixed and speller check enabled

### Changed
 - `prop` and `propOr` now accept opaque type keys
 - Debounce and throttle jsdoc improved with all params described
 - All predicate function now have proper jsodc
 - `Concat` jsdoc fixed

## 0.3.0 - 27-18-18
### Changed
 - Proper babel settings for es-build. (Browser env set to ie >= 11)

## 0.2.1 - 24-12-18
### Added
 - Alias support when used with `babel-plugin-lodash`

## 0.2.0 - 24-12-18
### Changed
 - ES build moved to root, only cherry-picked inner dependencies (to be compatable with `babel-plugin-lodash`)

## 0.1.1 - 18-12-18
### Changed
 - Inital types converted from $ReadOnlyArray to Array to match lodash typings (just before being replaced by ours)

## 0.1.0 - 18-12-18
### Changed
 - All lodash/fp usages changed to lodash
 - Minor fixes in typings of head, tail and prop to make it closer to native flow
 - Minor fixes in typings of sortBy, uniq to allow ReadOnlyArrays

### Added
 - Publish commands, es and commonjs builds
 - Lodash-babel-plugin for all builds
