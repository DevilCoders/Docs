mobile-yandex-mail-client-android
=================================

New Yandex.Mail for Android

## Installation

- Install `Android Studio` with associated tools. Choose latest Android SDK and latest Android API.
Project minimum Android API version is 21.
- Run `xcode-select --install` to install `XCode Command Line Tools` for `otool` program
- Open project in Android Studio from directory `arcadia/mobile/mail/android/mail-app`
- `Make project` several times until successful. `Refresh all Gradle projects` can help.
- Install emulator through `Tools -> ADV Manager`. Choose most simple device like `Nexus S` for speed.
- Run `app` on emulator
- You can login as `ttqul` user with password `qqqwww1`

## Glossary

- `fid` - folder id
- `mid` - message id
- `tid` - thread id
- `lat` - last access time
- `did` - draft id
- `aid` - account id
- `hid` - hierarchy id
- `uid` - user id

## Tanker

Our Tanker page:
https://tanker.yandex-team.ru/project/mobmailandroidphones?branch=master

How to pull new translations:
1. Configure tanker authorization https://tanker-guide.daas.yandex-team.ru/api/index.html#avtorizacija
2. run ./gradlew -b localize.gradle

For adding new keyset find:
`task localizeAndroid` in localize.gradle
## Other

API documentation:
https://pages.github.yandex-team.ru/Daria/mobile-api-docs/

Stories
https://wiki.yandex-team.ru/users/svyatoslavdp/marki-v-pochte/

Endpoint URL:
http://mail.yandex.ru/api/mobile/v1
http://mail.yandex.ru/api/mobile/v2

Push API:
https://console.push.yandex-team.ru

#### How to update JavaScript part of the Yandex.Mail for Android
Use the script `update-react.sh`
