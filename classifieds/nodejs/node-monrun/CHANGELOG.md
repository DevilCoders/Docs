# Changelog

## UNRELEASED

## 0.3.0 - 2016-06-20

### Added

- Add `opts.expire: Number = 3.6e+6` to the `Check` constructor.
  Both `Check#pass()` and `Check#fail()` record current time. If the time is earlier than `opts.expire`,
  the particular status is considered to be expired and does not taken into account during `Check#status()`
  calculation.

## 0.2.2 - 2016-06-01

### Bug fix

- The status of the `Check` wasn't replaced properly by a new status.

## 0.2.1 - 2016-05-17

### Other changes

- Result of `monrun.status()` doesn't match to the shape described in docs.

## 0.2.0 - 2016-05-17

### Breaking changes

- `Check#status()` returns `Status`, e.g. an object with the shape `{ code: Number, message: String, label: String }`.
- `monrun.status()` returns a status as an object `{ code: Number, statuses: Array<Status> }`.

### Other changes

- `Check#fail()` accepts an error message as an argument.

## 0.1.0 - 2016-05-16

- Initial release.
