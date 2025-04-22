Тест для проверки работы typeinfo между динамическими библиотеками под android. Необходимо собирать с флагом `MAPS_MOBILE_EXPORT_CPP_API`.

Пример команды сборки:

`ya make --maps-mobile -ttt --target-platform=default-android-armv8a -DMAPS_MOBILE_EXPORT_CPP_API`

Описание проблемы: https://android.googlesource.com/platform/ndk/+/master/docs/user/common_problems.md#rtti_exceptions-not-working-across-library-boundaries



