# Yandex IO SDK for Android

YandexIO в .aar для дистрибуции на Android девайсы без root доступа.

## Детали

### Нативная часть

1. `cpp/launcher` - Android-лончер для Yandex IO SDK
2. `cpp/jni` - jni-прослойка для вызова Yandex IO SDK из Android-приложения
3. `config` - собирается в `quasar.cfg`
4. `data` - содержит звуки и модели споттеров

### Java часть

Весь код java-части находится в проекте `java/yandex_io_sdk`. При сборке он берёт все детали из нативной части и собирает их в `.aar`-библиотеку, которую можно использовать в `.apk`.

1. `ru.yandex.io.sdk` - публичное api
2. `ru.yandex.io.sdk.jni` - jni обертки
3. `ru.yandex.io.sdk.audio` - запись звука с микрофона

## Сборка

- `native_android` - из `cpp/launcher` и `cpp/jni` собирается `libquasar_daemons.so`. Также собираются `config` и `data`, чтобы их можно было подключить к `.aar`.
- `native_linux` - собирает то же, что и в `libquasar_daemons.so`, но в виде исполняемого файла для Linux.
- `libs` - собирает нативные библиотеки, от которых зависит `libquasar_daemons.so`.
- `aar` - из результата сборки `native_android` и Java-части собирает `yandex-io-sdk.aar`.

Проект `yandex-io-sdk` можно подключить в сторонний Gradle build и собирать из Android Studio, предварительно собрав бинарники. Пример интеграции есть в `$A/smart_devices/android/tv/services/services-iosdk-app`.

Подробную схему сборки см. тут: https://wiki.yandex-team.ru/quasar/yandex_io_aar/

### Разное полезное

Погенерить jni хэдеры

```
./gradlew :yandex-io:sdk:generateJniHeaders
```
