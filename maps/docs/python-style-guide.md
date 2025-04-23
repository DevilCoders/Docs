# Geo-infra Python Style Guide

Geo-infra team has adopted some standard python style guide rules and 
applied them to its python project - SEDEM.
This document consists of remarks to the adopted [Google Style Guide](https://google.github.io/styleguide/pyguide.html). 

**To make it easier to reference and navigate through remarks of 
the style guide we keep numeration the same.**

## 1 Background 

This style guide is a list of *dos and don'ts* for Python programs.

Geo-infra team uses the [yapf](https://github.com/google/yapf/)
auto-formatter to avoid arguing over formatting.

### 1.1 Adding pylint to your tests

To use geo-infra python style guide, add to your tests ya.make file the following lines:
```yamake
SET(TARGET_PYLINT_FOR maps/path/to/your/lib)  # Takes all PY_SRCS for linting.
SET(TARGET_PYLINT_CONF maps/pylibs/recipes/pylint/pylintrc)  # You can create your own.
SET(TARGET_PYLINT_CQA 9.0)  # Check score from 0 to 10. See description of the score below.
# And path to pylint template.
INCLUDE(${ARCADIA_ROOT}/maps/pylibs/recipes/pylint/test.inc)

# We recommend to run them in medium suite, to hide output while running small tests.
SIZE(MEDIUM)
```
To see pylint report, you can run the following command in your tests directory: 
`ya make -tt -F=pylint_test.py*`

### 1.2 Code quality agreement (CQA)

Code quality agreement is a parameter for pylint metric that is used to
fail pylint test check if a given module violates the CQA. The number is computed
by pylint, depending on the config (pylintrc). The highest score is 10.0 points that are
 given for full compliance with the config. And the lowest is 0.0 (I don't think your
 code even runs in this case).

For example the output:
```text
************* Module maps.infra.sedem.lib.tracker2.lowlevel
Score >= threshold: 9.444444444444445 >= 9.0
C:104, 0: Unnecessary parens after 'not' keyword (superfluous-parens)
W: 59, 8: Attribute 'trigger_action' defined outside __init__ (attribute-defined-outside-init)
W: 69,20: Attribute 'auxiliary_db' defined outside __init__ (attribute-defined-outside-init)
R:133, 4: Either all return statements in a function should return an expression, or none of them should. (inconsistent-return-statements)
W:147,12: Attribute 'conf_id' defined outside __init__ (attribute-defined-outside-init)
C:177, 8: Attribute name "rm" doesn't conform to '[a-z_][a-z0-9_]{2,}$' pattern (invalid-name)
W:182, 8: Attribute 'branch_version' defined outside __init__ (attribute-defined-outside-init)```
```
Doesn't violate the metric with a score of 9.4.

### 2.12 Default Argument Values 

#### 2.12.5 Remark

Using logical operators instead of if statements is also okay.

```python
Yes: def foo(a, b: Optional[Sequence] = None):
         b = b or []
```

### 2.19 Power Features 

#### 2.19.5 Remark 

Avoid these features in your code, unless you are writing some general library 
that will be easier to use.

### 2.21 Type Annotated Code 

Stub files currently are not supported by our ya.make builds, so they can 
only be used for IDE features.

## 3 Python Style Rules 

### 3.2 Line length 

_Recommended_ line length is *80 characters*.

Maximum line length is *120 characters*.

### 3.7 Shebang Line 

In Arcadia, shebang lines are useless and discouraged to use in `.py` files, 
as python code SHOULD NOT be executed directly without being compiled with ya make first.                                                                             

### 3.8 Comments and Docstrings 

#### 3.8.2 Modules (remark)

We encourage to start files with a docstring describing the contents and usage of the
module, but it is not required.
