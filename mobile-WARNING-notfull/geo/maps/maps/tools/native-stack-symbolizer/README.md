## Requirements

- NDK (`ANDROID_NDK_HOME` should be exported)
- wget (available in `PATH`)
- unzip (available in `PATH`)
- pbpaste (available in `PATH`)

## Usage

### Without installation (Gradle Run)

```sh
cd tools && ./gradlew :native-stack-symbolizer:run -q --args="<options>"
```

### With installation

1. Install:
```sh
cd tools && ./gradlew :native-stack-symbolizer:installDist
export PATH="$PATH:$(realpath tools/native-stack-symbolizer/build/install/native-stack-symbolizer/bin)"
```

2. Use:
```sh
native-stack-symbolizer <options>
```

⚠️ Warning ⚠️

When compiling, the version of MapKit from `DependenciesHolder` is inserted into binary. To update it, you should recompile.

## Options

```sh
> cd tools && ./gradlew :native-stack-symbolizer:run -q --args="--help"
Usage: native-stack-symbolizer options_list
Options:
    --from-clipboard -> Take stacktrace from clipboard
    --from-file -> Take stacktrace from file { String }
    --from-stdin -> Take stacktrace from stdin
    --symbols-paths -> Paths to seek symbols in format 'path1,path2,path3'. Path can be a directory or a simple file { String }
    --maps-mobile-version -> Version of Maps Mobile native library to seek symbols. If not supplied, version from DependenciesHolder is taken { String }
    --abi -> Suggested ABI. If not supplied, try to infer ABI from stacktrace { String }
    --address-offset -> Global address offset. Minus sign is accepted { String }
    --help, -h -> Usage info
```

## Symbols cache

The tool uses `~/.maps-mobile-symbols-cache` to store Maps Mobile symbols. You may want to clear it occasionally.

Clear:

```sh
rm -rf ~/.maps-mobile-symbols-cache
```

## Examples

From clipboard using version `2020121119.7714926-navi` and armeabi-v7a:
```sh
cd tools && ./gradlew :native-stack-symbolizer:run -q --args="--from-clipboard --maps-mobile-version=2020121119.7714926-navi --abi=armv7"
```

From file `stacktrace.txt` using version `2020121119.7714926-navi` and armeabi-v7a:
```sh
cd tools && ./gradlew :native-stack-symbolizer:run -q --args="--from-file=stacktrace.txt --maps-mobile-version=2020121119.7714926-navi --abi=armv7"
```

From file `stacktrace.txt` (using stdin) using version `2020121119.7714926-navi` and armeabi-v7a:
```sh
cd tools && ./gradlew :native-stack-symbolizer:run -q --args="--from-stdin --maps-mobile-version=2020121119.7714926-navi --abi=armv7" < stacktrace.txt
```

From logcat:
```sh
adb logcat | cd tools && ./gradlew :native-stack-symbolizer:run -q --args="--from-stdin"
```

Just download `2020121119.7714926-navi` to symbol cache:
```sh
cd tools && ./gradlew :native-stack-symbolizer:run -q --args="--maps-mobile-version=2020121119.7714926-navi"
```
