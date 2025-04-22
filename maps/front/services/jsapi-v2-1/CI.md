# CI

This very document describes how continous integration for JSAPI works.

## Build

Build will run every time somebody pushes commit to the branch with name like `2.1*` and with commit message like `v2.1(rest-of-proper-version)`.

## Tests

Tests will run every time somebody pushes commit to the branch with names like [`2.1*`, `ci-debug/*`] or created a pull request.

