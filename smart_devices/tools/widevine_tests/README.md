Widevine LVL1 test tools
========================

See https://st.yandex-team.ru/QUASAR-7428

ExoplayerDemo
-------------

Bundled version is built from https://github.com/google/ExoPlayer/tree/r2.11.1 via
```
./gradlew :demo:assembleNoExtensionsDebug
```

Usage
-----

1. `pip install -r requirements.txt`
2. plug in DUT, make sure it is the only device
3. start `adb logcat EventLogger:V *:E` is a separate shell
4. run `py.test`
5. Observe the HDMI output and answer to the tests' questions
