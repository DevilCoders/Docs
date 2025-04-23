# GLAGOL dev repo
https://a.yandex-team.ru/arcadia/smart_devices/android/glagol

# Library
see glagol-sdk/README.md

# Demo app
Yandex wiki link:
https://nda.ya.ru/t/G0hqicnT5DEVDN

## Link to most recent GlagolDemoApp
https://nda.ya.ru/t/ckufMDtn57mNKv

## How to build
```bash
( ./gradlew clean assembleRelease )
( cd android-demo && jarsigner -verbose -keystore ~/.android/debug.keystore -storepass android -keypass android build/outputs/apk/release/android-demo-release-unsigned.apk androiddebugkey )
export ANDROID_SERIAL=<test_device> && adb uninstall ru.yandex.quasar.glagoldemoapp && adb install android-demo/build/outputs/apk/release/android-demo-release-unsigned.apk && adb shell am start -n ru.yandex.quasar.glagoldemoapp/.MainActivity
```

Optionally, you can pass OAuth token via adb when starting activity via intent extras like `adb shell am start -n ru.yandex.quasar.glagoldemoapp/.SelectorActivity --es "oauth_token" "AQAAAA......"`.

## How to get OAuth token

* In incognito mode go to https://oauth.yandex.ru/authorize?response_type=token&client_id=715e28401be542338a6a110734f36181
* Login into your Yandex test account
* Allow application to access your account info
* Have fun

