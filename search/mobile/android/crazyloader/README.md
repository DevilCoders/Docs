# CrazyLoader

- кастомный загрузчик `.so`-библиотек. Предназначен для загрузки `.so`, слинкованных с packed relocations для версий младше Android 6.0 Marshmallow
- основан на проекте [CrazyLinker](https://chromium.googlesource.com/chromium/src.git/+/master/third_party/android_crazy_linker/README.chromium)
- [contrib/libs/android_crazy_linker](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/libs/android_crazy_linker)

## Packed Relocations
- уменьшает размер бинарника **~3-3.5 Mb**
- `LDFLAGS(-Wl,--pack-dyn-relocs=android)`
- https://reviews.llvm.org/D39152
- [README от Google](https://android.googlesource.com/platform/bionic/+/f5e0ba94d911ef2622ecfd3f7fabc4432a4806d3/tools/relocation_packer/README.TXT)
- на Android 6+ работает из коробки

## Побочные эффекты
- https://chromium.googlesource.com/chromium/src.git/+/master/third_party/android_crazy_linker/src/README.TXT#Caveats
- требуется явная регистрация нативных методов в `JNI_OnLoad`: `Env->RegisterNatives()`

## Решение
- [search/mobile/android/crazyloader/lib](https://a.yandex-team.ru/arc/trunk/arcadia/search/mobile/android/crazyloader/lib) — обертка вокруг CrazyLinker с поддержкой регистрации методов и загрузкой основной библиотеки, слинкованной с packed relocactions
- автогенерация кода для регистрации на основе `.jar` файла с классами-обёртками нативных вызовов (к примеру, генерируемых SWIG проектом `DLL_JAVA`)
- [search/mobile/android/crazyloader/codegen](https://a.yandex-team.ru/arc/trunk/arcadia/search/mobile/android/crazyloader/codegen) — Java проект для генерации кода
- [dict/mt/libs/mobile/android/crazyloader](https://a.yandex-team.ru/arc/trunk/arcadia/dict/mt/libs/mobile/android/crazyloader) — пример проекта динамической `.so`

#### Что нас временно отделяет от стройного красивого решения:

- DEVTOOLSSUPPORT-5961 / DEVTOOLS-6399 / DEVTOOLS-7173 — текущие проблемы с вызовом Java модулей для кодогенерации в C++ проектах в Аркадии
- workarounds
  - DEVTOOLS-7774 — новые макросы для Java
    - требуется использование новых макросов `JAR_PROGRAM` / `JAR_LIBRARY` / `RUN_JAR_PROGRAM`
    - Генератор сделан с макросом `JAR_PROGRAM`
    - Вызывается через `RUN_JAR_PROGRAM`

  - DEVTOOLS-7987 — не готова поддержка `UBERJAR` 
    - на вход кодогенератору подаются отдельные `.jar`-ники от всех требуемых проектов
    - клавиатурный `.jar`-ник строится отдельным временным модулем `JAR_LIBRARY`
