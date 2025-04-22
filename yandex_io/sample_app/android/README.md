## Встраивание YandexIO в Android приложения

Содержимое:
- `launcher` - библиотека, позволяющая запускать все нужные компоненты quasar в
  одном процессе.
  - `launcher/example` - программа на C++, позволяющая запустить quasar.
- `jni` - JNI обертка к `launcher`
  - `jni/example` - библиотека и тестовое приложение для запуска quasar из JVM.
- `example_app` - минимальное Андроид-приложение, запускающее quasar.

### Запуск на Яндекс.Станции

1. Собрать JNI модуль в `src/platforms/android_app/jni/example`. В результате
   получаются два файла: `jni-example.jar`, `jni-example/libquasar_launcher_jni.so`.
   - Сборка под x86: `ya make -D JDK_VERSION=8`
   - Сборка под Яндекс.Станцию: `ya make --target-platform gcc49-android-armv8a -D USE_STL_SYSTEM -D OS_SDK=ubuntu-16 -D YANDEXSTATION -D JDK_VERSION=8`
2. Положить `libquasar_launcher_jni.so` в `/system/vendor/quasar`.
3. Собрать APK (при этом используется `jni-example.jar` с первого шага).
4. Подготовить Яндекс.Станцию к запуску:
  - "Удалить" приложения Quasar: `mkdir /system/disabled-app && mv /system/priv-app/Quasar-* /system/disabled-app`.
  - Положить симлинки на библиотеки quasar в `/vendor/lib64`:
    ```
    libapr-1.so.0 -> /system/vendor/quasar/libs/libapr-1.so.0
    libaprutil-1.so.0 -> /system/vendor/quasar/libs/libaprutil-1.so.0
    libavahi-common.so -> /system/vendor/quasar/libs/libavahi-common.so
    libavahi-core.so -> /system/vendor/quasar/libs/libavahi-core.so
    libgnustl_shared.so -> /system/vendor/quasar/libs/libgnustl_shared.so
    libiconv.so -> /system/vendor/quasar/libs/libiconv.so
    libintl.so -> /system/vendor/quasar/libs/libintl.so
    libjansson.so -> /system/vendor/quasar/libs/libjansson.so
    libjsoncpp.so.11 -> /system/vendor/quasar/libs/libjsoncpp.so.11
    libjwt.so -> /system/vendor/quasar/libs/libjwt.so
    liblog4cxx.so -> /system/vendor/quasar/libs/liblog4cxx.so
    libopenal.so.1 -> /system/vendor/quasar/libs/libopenal.so.1
    libspeechkit.so -> /system/vendor/quasar/libs/libspeechkit.so
    libuuid.so.1 -> /system/vendor/quasar/libs/libuuid.so.1
    ```
  - Перезагрузить Станцию.
5. Запустить приложение `example_app` на Станции.
