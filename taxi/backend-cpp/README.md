<b> backend-cpp is now developed in arcadia </b>

Actual path is https://a.yandex-team.ru/arc_vcs/taxi/backend-cpp

<i>If you see any unactual information here, please fix it by yourself or with help of your chief/mentor.</i>

Responsible: Client product backend, client product infra

## Brief description

Services API and collections documentation can be found [here](<https://github.yandex-team.ru/pages/taxi/schemas/Taxi_Documentation/>).

* To build project you need clang (>=7.0)
* We use google style guide
* All important operations could be done using Makefile

## Makefile commands

- `make all` or `make` or `make build` - builds sources.
- `make run` - build sources and run fastcgi-daemon with compiled lib using
configs from `manual` folder.
- `make test` - build and run tests.
- `make clean` - remove `build` directory
- `make check-pep8` - run flake8 against testsuite
- `make smart-check-pep8` - run flake8 against changed python files
- `make format` - run taxi formatter
- `make smart-format` - run taxi formatter only on changed files
- `make changelog` - helper to generate changelog file during building version
- `make deb` - make debian package in parallel
- `make setup-git-hooks` - install pre-commit hooks for formatting changed files before commit
- `make setup-git-hooks-extended` - install pre-commit hooks for formatting and running linters on changed files before commit

## How to run testsuite

Install packages required to run testsuite.

### Ubuntu

```bash
# Python dependencies
sudo apt-get install taxi-deps-py3-2

# Related services
sudo apt-get install nginx mongodb redis-server postgresql-10
```

Install specific "yandex" nginx version:

```bash
sudo apt install nginx-common=1.8.1-1.yandex.24
sudo apt install nginx-full=1.8.1-1.yandex.24

```

### MacOS X

```bash
# Install python dependencies using pip into your system or virtualenv.
pip3 install -i https://pypi.yandex-team.ru/simple/ -r testsuite/requirements.txt

# Manually install related services and databases:
# nginx mongodb redis-server postgresql-9.5
```

### Data files

Copy libgeobase6 binary files from testing to your local machine:

- /var/cache/geobase/geodata4.bin
- /var/cache/geobase/geodata4.bin.patch


### MongoDB ramdisk

Mount ramdisk (just for fix test timeouts):

```(bash)
$ echo -e '\nnone /mnt/ramdisk tmpfs defaults 0 0' >> /etc/fstab
$ mount -a
```

### Running testsuite
Testsuite is enabled by default. For local development useful to have
`CMAKE_BUILD_TYPE` variable set to `Test`. This disables compiler
optimizations and enables debug information (`-O0 -g3`).

```
backend-cpp$ rm -rf build
backend-cpp$ make BUILD_TYPE=Test
```

After project is compiled you can run tests with `ctest` command:

```
build$ ctest -V
```

### Start py.test manually

```
backend-cpp$ ./build/testsuite/runtests -vv ./protocol/lib/testsuite/protocol/test_launch.py 
```

### GDB + py.test

In case you dont't want to run the whole testsuite and you whant to run specific testcase you have to start testing environment with `taxi-protocol` launched in gdb for instance:

```
build$ ../build/testsuite/taxi-env run -- \
    gdb --args fastcgi-daemon2 --config=testsuite/configs/taxi-protocol.conf
...
Starting mongo, nginx here, creating indexes...
Don't mind about nginx error message it's ok
...
(gdb)
```

Currently `taxi-protocol` does not support ondemand reload of all the cached data so you have to load mongo fixtures first:

```
testsuite$ ../build/testsuite/runtests --fastcgi-disable --no-env ./tests/
```

That would fail but after that you can start fastcgi daemon:

```
(gdb) r
Starting program: /usr/sbin/fastcgi-daemon2 --config=testsuite/configs/taxi-protocol.conf
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
```

After that you can run tests with regular `runtests` with `--fastcgi-disabled' which disables fastcgi daemon spawning:

```
testsuite$ ../build/testsuite/runtests --fastcgi-disable ./tests/test_launch.py
```

### Enabling and disabling ccache

There is ccache support via cmake variables. To enable ccache in your build set variable `USE_CCACHE` to 1:
```
CMAKE_OPTS="-DUSE_CCACHE=1" make
```
To properly disable ccache you shou;d set variable to zero, otherwise it can be cached. so, at least once you should run:
```
CMAKE_OPTS="-DUSE_CCACHE=0" make
```
To enable ccache support in CLion, go to File -> Settings -> Build, Execution, Deployment -> CMake and add `-DUSE_CCACHE=1` to CMake options.

---
---
---
