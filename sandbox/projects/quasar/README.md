# Сборка Яндекс.Станции (Квазар)

См https://st.yandex-team.ru/QUASAR-602 / https://st.yandex-team.ru/QUASAR-616

## Структура

* сборка выполняется в [Sandbox](https://sandbox.yandex-team.ru/)'е ([wiki](https://wiki.yandex-team.ru/sandbox/))
* состоит из таких [задач](https://sandbox.yandex-team.ru/tasks?owner=QUASAR):
    - `QUASAR_BUILD_IMAGE` -- собирает прошивку и ОТА-бандлы
    - `QUASAR_BUILD_SERVICES` -- собирает Java и C++-сервисы
    - `QUASAR_BUILD_FULL` -- собирает "всё", запуская предыдущие две задачи "в связке", и переводит собранные артефакты в статус `релиз`
* артефакты сборки публикуются [ресурсами](https://sandbox.yandex-team.ru/resources?owner=QUASAR):
    - `QUASAR_DEVICE_IMAGE` -- полный образ для прошивки устройства
    - `QUASAR_OTAIMAGE` -- .zip-архив для ОТА-обновления
    - `QUASAR_LINUX_IMAGE` -- образ для прошивки устройства, содержащий только раздел с Linux'ом
    - `QUASAR_DAEMONS` -- все C++-севисы и конфиги
    - `QUASAR_APP` -- `quasar-app.apk`
    - `QUASAR_SERVICES` -- `quasar-services.apk`
* `QUASAR_DEVICE_IMAGE` / `QUASAR_OTAIMAGE` собираются в двух вариантах -- `builtype=eng` и `buildtype=userdebug`, для первого используются `dev`-конфиги, для второго -- `prod`;
* сборка запускается:
    - `QUASAR_BUILD_IMAGE` -- по коммиту в мастер [основного репозитория](https://bb.yandex-team.ru/projects/QUAS/repos/r18stationandroid/) при помощи [TeamCity](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Quasar_R18imageBuild_BuildFullImage) (который поллит репозиторий)
    - `QUASAR_BUILD_SERVICES` -- по коммиту в [репозиторий сервисов](https://github.yandex-team.ru/quasar-dev/quasar/) про помощи GitHub-хуков, которые слушает [сервис Sandbox-CI](https://github.yandex-team.ru/search-interfaces/microservices/blob/master/services/sandbox-ci/docs/universal.md). Конфигурация запуска хранится в [самом репозитории](https://github.yandex-team.ru/quasar-dev/quasar/blob/master/.config/sandbox-ci.json)
    - `QUASAR_BUILD_FULL` -- [sandbox-планировщиком](https://sandbox.yandex-team.ru/scheduler/8474/view) в полночь каждого дня для сборки `master`-веток

## Где взять свежие сборки

Свежие сборки из master-веток можно найти так:
* найти все [свежие ресурсы, которые были зарелижены](https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&attrs=%7B%22released%22%3A%22stable%22%7D&owner=QUASAR&order=-id)
* выбрать среди них ресурс с нужным типом и атрибутами (например, у `QUASAR_OTAIMAGE` есть атрибуты `buildtype` и `version`) -- например, [ресурс 507147224](https://sandbox.yandex-team.ru/resource/507147224/view)
* на его странице найти ссылки на скачивание с HTTP Proxy -- например, [https://proxy.sandbox.yandex-team.ru/50714722](https://proxy.sandbox.yandex-team.ru/507147224)

## Версионирование

* у каждой компоненты (android'а и сервисов) есть своя версия из 2х частей (`major.minor` -- например, `1.7`)
* она записана в файле `VERSION` в корне соответствующего репозитория и ведется вручную, отражая функциональность, аналогично схеме semver. Т.е. при добавлении новой фичи мы бампаем минорную часть, при добавлении большой фичи / большого рефакторинга / обратно-несовместимых изменений -- бампаем мажорную часть.
* суммарная версия прошивки формируется по схеме `{android.major}.{services.major}.{android.minor}.{services.minor}.{build_id}` -- где версия андроида это `{android.major}.{android.minor}`, а версия сервисов -- `{services.major}.{services.minor}`. Например, для версий `1.10` и `2.35` соответственно версия прошивки может быть `1.2.10.35.222725915`
* в исходниках указанную явно версию заменим на плейсхолдер `__QUASAR_VERSION_PLACEHOLDER__`
* суммарная версия пишется в файл version_full рядом с демонами
* `VERSION` сервисов будет собираться вместе с ними в артефакт и приноситься на сборку прошивки
* в таске `QUASAR_BUILD_IMAGE` общая версия формируется из той, что лежит в репозитории (андроид) и той, что приехала в ресурсе `QUASAR_DAEMONS` (сервисы), плюс происходит подмена версий во всем каталоге `R18_android/android/device/softwinner/tulip-d1` (где и живут квазаро-специфичные части прошивки)
