NOTE: RU version is more full and actual version

# Tap Config
Test your frontend just with yaml config.
Tool is based on selenium and launches tests in [TAP philosophy](https://testanything.org/). 

# Guide

## Pah tests

## log
```
log:
    level: error
    like: Focused
```

### wait
```
options:
  timeout: 10

tests:
  - get_ok: /base.html
  - wait:
      - has: xpath:/html/body
      - has: css:p#text
```

Notation is pretty the same as
[the short one](https://github.yandex-team.ru/andrew-zak/pahtest#short-wait-notation-for-active-test) for wait utility.


## Utils

### wait
Wait test has two different notations for active tests. And one for passive tests:
```
options:
  timeout: 10

tests:
  - get_ok:
      wait:  # long notation for active test
        timeout: 10
        description: Wait until page has body and some text
        tests:
          - has: xpath:/html/body
          - has: css:p#text
  - get_ok:
      wait:  # short notation for active test
        - has: xpath:/html/body
        - has: css:p#text
  - has:  # notation for passive test
      xpath: /html/body
      wait: 10  # just seconds in float types
```

Both active test notations contain subtests. Those ones can be only passive.
Active tests inside wait subtests will lead to error.

Note that short notation for active test has no description.
Wait section will take description from it's first subtest.


#### Ref for "wait" option
TODO - describe inner waiting mech. Maybe forward "step" param to the options.

##### Long wait notation for active test
- description - optional
- timeout - optional, float type or "default" string.
  If timeout is empty or has "default" value, options.timeout value will be taken.
- tests - required. Has pretty the same notation as global "tests" section except of one point:
  *wait section can contain only passive subtests*.
  
##### Short wait notation for active test
It's body - list of subtests. See "tests" option in below notation for details.
If notation has no description it will be taken from the first subtest.

##### Wait notation for passive test
Accepts one value for timeout. See "timeout" option in below notations for details. 


# For dev

## Launch tests for plugin
You can launch separated test for a single plugin with it's id:
```
pytest -sv tests/ -k test_click_ok
```
`test_click_ok` test id created corresponding file `tests/assets/plugins/click_ok`.

Short notation will also work since `click_ok` is substring of `test_click_ok`:
```
pytest -sv tests/ -k click_ok
```


## Subtests tap out
in wait too
```
ok 5 - какой-то тест перед wait
   1..2
   ok 1 - первый сабтест
   ok 2 - второй сабтест
ok 6 - результаты wait
```
