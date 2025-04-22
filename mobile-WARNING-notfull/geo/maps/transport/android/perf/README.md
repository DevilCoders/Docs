See https://wiki.yandex-team.ru/pulse/perftests/writingperftest/

## How to run locally
1. You need either an emulator or real device with recent API level (16 and up)
   with root available (NOT su, `adb root` should succeed restarting adbd with
   root permissions). Usually this means that userdebug build must be installed.
   Linux hosts are fully supported, MacOS support is experimental.
2. (This and the following steps assume we're running from repository root)
   Create a virtualenv and activate it:
    ```
    virtualenv -p python2 .venv && source .venv/bin/activate
    ```
   Note: if `virtualenv` reports that there is no `python2` binary found, you
   can use the command without `-p python2` argument.
3. Install perf dependencies into newly-created virtualenv:
    ```
    pip install -r perf/requirements.txt
    ```
4. Set the variable `$DEVIL_FORCE_ADB` to point to `adb` binary you're using to
   access devices. If you use `adb` from system path, run
    ```
    export DEVIL_FORCE_ADB=$(which adb)
    ```
5. Run some benchmark:
    ```
    python -m catapulse.run_benchmark perf run --device=$DEVICE $BENCHMARK
    ```
   Here `$DEVICE` denotes serial id of your connected device or emulator, and
   `$BENCHMARK` is the name of benchmark you want to run.
   e.g.
    ```
    python -m catapulse.run_benchmark perf run --device=emulator-5554 ru.yandex.yandexbus.perf.tests.AppStartupTest
    ```

   All the discovered benchmarks can be printed out with `print_metadata`
   command:
    ```
    python -m catapulse.run_benchmark perf print_metadata --device=$DEVICE
    ```
   For instrumented tests the name of benchmark is the full name of test class,
   for example, `com.yandex.mail.perftests.runner.MailTest`.
6. You may wish to add `--output=$OUTPUT` to write results to `$OUTPUT`
   directory in yajson format (see `$OUTPUT/results.ya.json`). This directory
   will be created automatically after the run. You may also change the number
   of repetitions with `--repeat=$NUM` parameter.

## Shortcomings
1. Catapulse can't recognize rooted emulator,
   so you should manually change `ls /root` in
    ```
    catapulse/devil/devil/android/device_utils.py
    ```
   to something like `ls /data/data/`

2. One should also add `.inhouse` to package in instrumented.py
   in order to instrument local builds with python (launching with studio is unaffected)
