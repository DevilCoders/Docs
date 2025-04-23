# Android platforms

Source code for Android libraries containing different Yandex IO capabilities.

## Publish

To publish to local maven repository, run:

```bash
./gradlew publishToMavenLocal
```

## Versioning

Specify version in [`version.gradle`](./version.gradle)


## Sample app

App that integrates parts of `yandex-io-android-sdk`.


### Build for emulators

Assemble [`sample-app](sample-app) for x86 architecture:

```bash
./gradlew :sample-app:assembleX86Debug
```

Install:

```bash
adb install -r sample-app/build/outputs/apk/x86/debug/sample-app-x86-debug.apk
```

### Build for devices

Assemble [`sample-app](sample-app) for aarmv8 architecture:

```bash
./gradlew :sample-app:assembleAarmv8Debug
```

Install:

```bash
adb install -r sample-app/build/outputs/apk/aarmv8/debug/sample-app-aarmv8-debug.apk
```
