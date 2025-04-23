## Подготовка
- `sudo apt-get install devscripts`
- `sudo mk-build-deps -i`
- `./build_google_mock.sh`
- `pip install pymongo==3.5.1`

## Сборка
- `MONGO_USER=<user> MONGO_PASSWORD=<password> make driver` - собрать библиотеки mongocxx драйвера
- `make build` — собрать библиотеку локализаций

## Тесты
- `MONGO_USER=<user> MONGO_PASSWORD=<password> make tests`

## Сборка deb-пакета
- `MONGO_USER=<user> MONGO_PASSWORD=<password> debuild --preserve-env` - собрать пакет
- `debrelease --to yandex-mobile-xenial` - залить пакет в репо

В конце 2х последних шагов ожидаются записи типа `Ok`, говорящие о том, что все тесты прошли на ура и мы идем правильным путем.

## Старое общее описание (требует актуализации)
[wiki-страница](https://wiki.yandex-team.ru/yandexmobile/server/libs/sharedlocalization/)

## Описание конфига (требует актуализации)
[wiki-страница](https://wiki.yandex-team.ru/yandexmobile/server/libs/sharedlocalization/config/)

## Описание полной сборки экспериментов
[wiki-страница](https://wiki.yandex-team.ru/yandexmobile/advisor/experiments/buildoldway/)
