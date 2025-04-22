# Smart Devices (Android)

Contains Android code to be used together with **yandex_io** https://a.yandex-team.ru/arc/trunk/arcadia/yandex_io to
create Yandex smart devices and SDKs to include in other applications to iterate with them.

It includes:
- Smart Speakers
- TVs
- Smart Screens
- Glagol SDK

## Development

There's different products supported. Refer to [**settings.gradle**](https://a.yandex-team.ru/arc_vcs/smart_devices/android/settings.gradle#L6).
Product should be provided in local.properties as (example) `product=quasar` which will ensure only needed modules are included in Android Studio project and during the build.
