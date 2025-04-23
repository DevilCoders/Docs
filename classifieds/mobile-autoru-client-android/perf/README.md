## Overview

This directory contains various files needed to run performance tests
using Pulse test infrastructure. See wiki for more information about Pulse:
https://wiki.yandex-team.ru/pulse/

The tests (also called *benchmarks*) are run with
[catapulse](https://pypi.yandex-team.ru/repo/default/catapulse/) Python
library based on [catapult](https://github.com/catapult-project/catapult)
project.

## Directory structure

- `benchmarks`: this directory contains descriptions for all the tests to be run
  as performance benchmarks. Now the most useful file here is
  `benchmarks/instrumented.py`, which defines all the benchmarks that are run as
  instrumented Android tests from `ru.auto.ara.perftests.runner.test`
  package.
- `archives`: this directory contains links to WPR archives (`*.wprgo.mds`) to
  be used for mocked HTTP responses while running benchmarks. Archives
  themselves are not checked-in and downloaded on demand before benchmarks run.
  Archive files use `*.wprgo` extension with the same base name.

## How to run locally

1. You need either an emulator or real device with recent API level (16 and up)
   with root available (NOT su, `adb root` should succeed restarting adbd with
   root permissions). Usually this means that userdebug build must be installed.
   Linux hosts are fully supported, MacOS support is experimental.

2. (This and the following steps assume we're running from repository root)
   Create a virtualenv and activate it:
    ```
    python2 -m virtualenv -p python2 venv
    source venv/bin/activate 
    ```

3. Install perf dependencies into newly-created virtualenv:
    ```
    (venv) $ pip install -r perf/requirements.txt
    ```

4. Set the variable `$DEVIL_FORCE_ADB` to point to `adb` binary you're using to
   access devices. If you use `adb` from system path, run
    ```
    (venv) $ export DEVIL_FORCE_ADB=$(which adb)
    ```

5. Run some benchmark:
    ```
    (venv) $ python -m catapulse.run_benchmark perf run "--device=$DEVICE" "$BENCHMARK"
    ```
   Here `$DEVICE` denotes serial id of your connected device or emulator, and
   `$BENCHMARK` is the name of benchmark you want to run.

   All the discovered benchmarks can be printed out with `print_metadata`
   command:
    ```
    python -m catapulse.run_benchmark perf print_metadata "--device=$DEVICE"
    ```
   For instrumented tests the name of benchmark is the full name of test class,
   for example, `ru.auto.ara.perftests.runner.MainTest`.

6. You may wish to add `--output=$OUTPUT` to write results to `$OUTPUT`
   directory in yajson format (see `$OUTPUT/results.ya.json`). This directory
   will be created automatically after the run. You may also change the number
   of repetitions with `--repeat=$NUM` parameter.
   
7. Finally run command, for deactivation:
    ```
    (venv) $ deactivate
    ```
