Mainframer setup instruction can be found [here](https://wiki.yandex-team.ru/disk/mobile/android/#mainframer)

Copy mainframer-init.sh to disk android dir:
```
cp ../../workflow/android/mainframer-init.sh ./mainframer-init.sh
```
After initialization move mainframer.sh and .mainframer/ to the /mobile/ folder
```
mv ./mainframer.sh ../../../mainframer.sh
mv .mainframer ../../../.mainframer
```
Sign QA and Release builds:
get token [here](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=221cc392f0124696ae0d819b0e9bf954)
put token into yandex-signer.properties:
```
echo "oauth=YOUR_TOKEN" > "$HOME/.yandex/yandex-signer.properties"
```

Setup mobdisk team scripts:
```
brew install coreutils
../../workflow/install
```

Setup Startrek integration:
You can get token [here](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=69e08f5ae07442dbaafacbfe7f0b9145)
Save it:
```
echo token > ~/.yandex/st.token
```
Setup yt token (to report build time):
Go to [site](https://oauth.yt.yandex.net)
Follow instructions to get token and save it

Developer build:
```
sh monomainframer.sh ./gradlew app:assembleDevProdDebug \
 && adb install -r disk/android/disk-app/app/build/outputs/apk/devProd/debug/app-dev-prod-debug.apk \
 && adb shell am start ru.yandex.disk
```

If you need debug build for YPhone or Samsung with preinstalled Disk app you should use -PsignDebug=true
or set signDebug=true in gradle.properties
```
sh monomainframer.sh ./gradlew app:assembleDevProdDebug -PsignDebug=true \
 && adb install -r disk/android/disk-app/app/build/outputs/apk/devProd/debug/app-dev-prod-debug.apk \
 && adb shell am start ru.yandex.disk
```

Developer beta build:
```
sh monomainframer.sh ./gradlew app:assembleDevBetaDebug \
 && adb install -r disk/android/disk-app/app/build/outputs/apk/devBeta/debug/app-dev-beta-debug.apk \
 && adb shell am start ru.yandex.disk.beta
```

QA build:

```
sh monomainframer.sh ./gradlew app:assembleFatProdQa \
 && adb install -r disk/android/disk-app/app/build/outputs/apk/fatProd/qa/app-fat-prod-qa.apk \
 && adb shell am start ru.yandex.disk
```

Release build:
```
sh monomainframer.sh ./gradlew app:assembleFatProdRelease \
 && adb install -r disk/android/disk-app/app/build/outputs/apk/fatProd/release/app-fat-prod-release.apk \
 && adb shell am start ru.yandex.disk
```

Run test in core-test:
```
sh monomainframer.sh ./gradlew core-test:testReleaseUnitTest --tests ru.yandex.disk.YOUR_TEST
```

Run all tests:
```
sh monomainframer.sh ./gradlew testDebug jvmTest app:testDevProdDebug gallery:testProdDebug viewer:testProdDebug
```

Sync strings from tanker:
```
./tanker/downsync-all.sh
```
