# Testpy!

This library provides a way to run some linters over python source code in arcadia. Currently it includes:
  * doctest runner (for doctests from PY2_LIBRARY, not from PY2TEST)
  * pylint
  * flake8 (currently with experimental config)

# Common usage:
```cmake
PY2TEST()
SET(Y_TESTPY_FOR prj/my_py_lib)  # path for tested library
INCLUDE(${ARCADIA_ROOT}/prj/confs/common.ya.make.inc)
END()
````
# How to try:
For `prj/my_py_lib` run ya make -t on `prj/my_py_lib/testpy` with ya.make like:
```cmake
PY2TEST() # or PY3TEST() for python3
SET(Y_TESTPY_FOR prj/my_py_lib)
# ----------
# The following code is conveniently stored in a project include file
# ie prj/confs/all.ya.make.inc, prj/confs/doctest.ya.make.inc, etc
# !!! PLEASE USE YOUR OWN pylint/flake8 CONFIGS FOR NORMAL USAGE. !!!
# ----------
SET(Y_TESTPY_PYLINT_CONF prj/conf/pylintrc)  # for pylint only
SET(Y_TESTPY_FLAKE8_CONF prj/conf/flake8)  # for flake8 only
# some other options, see below
INCLUDE(${ARCADIA_ROOT}/ads/yacontext/lib/testpy/templates/testpy.ya.make.inc)
TEST_SRCS(
    doctest.py
    flake8.py
    pylint.py
)
FORK_TEST_FILES()
FORK_TESTS()
END()
```

# Options:
  * Y_TESTPY_FOR - path to target library (from arcadia root); python packages or sources will be auto detected from ya.make of this library
  * Y_TESTPY_NS - override auto detection from Y_TESTPY_FOR
  * Y_TESTPY_FLAT - disable runtime inspection of packages, use only explicitly defined sources
  * Y_TESTPY_PYLINT_CONF - path to pylint config (in source tree, without arcadia/ prefix)
  * Y_TESTPY_PYLINT_ARGS - extra args for pylint (ie --exclude=check_name)
  * Y_TESTPY_FLAKE8_CONF - path to pylint config (in source tree, without arcadia/ prefix)
  * Y_TESTPY_FLAKE8_ARGS - extra args for pylint (ie --exclude=check_id)
