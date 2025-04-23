**Android обёртка над С++ калькулятором**

Внутри директория ```/price-calc/src/main/cpp/price-calc``` это сабмодуль [price_calc](https://github.yandex-team.ru/taxi/price_calc/)
1. Обновить состояние сабмодуля на актуальное состояние(fetch & pull)

Чтобы обновить биндинги
1. Скачать проект [djinni](https://github.com/dropbox/djinni) - используется для генерации биндингов 
2. Из репы [price_calc_android_usage_sample](https://github.yandex-team.ru/ioann-v/price_calc_android_usage_sample) обновить содержимое файликов
- /price-calc/src/main/price_calc.djinni
- /price-calc/src/main/cpp/jni/impl.cpp
3. Запустить скрипт generate_jni_bindings.sh
```sh
DJINNI_PATH=path_to_djinni ./generate_jni_bindings.sh 
```

Чтобы собрать новый aar из исходников
```sh
./gradlew :price-calc:assembleRelease
```
Чтобы отправить собранный aar в artifactory(вместо звёздочек логин/пароль)
1. Положить в файлик local.properties креденшиалы учётной записи пользователя Такси в яндексовом артифактори(Узнать у Эда)
```sh
username=******
password=******
```
2. Запусить публикацию aar в артифактори(версия ставится в build.gradle файле)
```sh
./gradlew :price-calc:artifactoryPublish
```
