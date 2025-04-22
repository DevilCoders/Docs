init_subclass
======
Backwards compatibility for Python 3
[\_\_init_subclass\_\_](https://docs.python.org/3/reference/datamodel.html#object.__init_subclass__)
Use only with Python2 by adding in `ya.make`:

```yamake
IF(PYTHON2)
    PEERDIR(
        rt-research/common/pylib/init_subclass
    )
ENDIF()
```

Later will add full implementation (cls object and kwargs passing to function)

### Usage
```
class Philosopher(object):
    subclasses = []

    def __init_subclass__(cls, **kwargs):
        Philosopher.subclasses.append(cls.__name__)


class Socrates(Philosopher):
    pass
class Plato(Philosopher):
    pass


print Philosopher.subclasses
=> ['Socrates', 'Plato']
```