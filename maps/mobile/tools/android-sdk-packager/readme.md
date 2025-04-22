# How to update Android SDK

1. Update `BUILD_TOOLS_VERSION` in `package-android-sdk.sh`
2. Package new sandbox resources: `./package-android-sdk.sh`
3. Manually update [`ANDROID_SDK` in `build`](https://a.yandex-team.ru/search?search=%5CbANDROID_SDK%5Cb,%5Ebuild.*)
4. Update [`android_sdk_resource`](https://a.yandex-team.ru/search?search=android_sdk_resource): `./update-sandbox-resources.sh <LINUX-RESOURCE-ID>` 
5. Update [`targetSdkVersion`, `compileSdkVersion`, `buildToolsVersion`, `compileVersion`, `targetVersion`, `buildVersion` in `maps/mobile` and `build`](https://a.yandex-team.ru/search?search=targetSdkVersion|compileSdkVersion|buildToolsVersion|compileVersion|targetVersion|buildVersion,%5Emaps/mobile|^build): `./update-sdk-version.sh <BUILD-TOOLS-VERSION>`
6. Review it


*Note: `./update-sandbox-resources.sh` and `update-sdk-version.sh` works only with arc*

