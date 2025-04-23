SPECS CONSISTENCY LINTER
========================

## Tool for linting `.specs.js` && `.react.specs.js`

It checks that structure of unit-tests in different technologies are same.

*NB*: Don't use `it.only()` in jest specs. Use `xit` cause jasmine don't have such API.

## Example of usage:

```sh
# whole bem project
specs-consistency

# check specs of popup2
specs-consistency popup2

# By default we check only describe/it structure
# But with flag `--check-expect` you could lint them too
specs-consistency popup2_autoclosable_yes --check-expect

# `--warnings` flag will emit entities that has only `.react.specs.js` tests or only `.spec.js`.
specs-consistency checkbox__control --check-expect`
```

Use `--help` option for more details about command line usage.
