# TODO

* парсинг заголовков

# description
portal-morda-python-utils

# init dev environment
make dev
. venv/bin/activate

# requirements
python2.7

# testing
## python2
```
make test
```
## python3
```
PYTHON=python3 make test
```

# packaging

sudo apt-get install python-stdeb

```
python setup.py --command-packages=stdeb.command sdist_dsc
mv deb_dist/portal-morda-python-utils-1.0/debian .
```

# tar.gz

(venv) pip install distribute

make tar.gz

python setup.py sdist

# hints

```
python setup.py test
```

Run one test (ex. tests/test_utils.py)
```
python setup.py test -s tests.test_utils
```
