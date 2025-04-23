# Релизы мапкита в CI

[Подробная документация по релизам в CI](https://docs.yandex-team.ru/ci/release)

## Стадии релиза мапкита

Релиз состоит из четырех стадий:
1. **Подготовка релиза**. На этой стадии создается/обновляется релизный тикет и создается testpalm ветка.
2. **Сборка release candidate**. На этой стадии собираются тестаппы и загружаются на бету в release canditate ветки (релизные ветки с суффиксом `_rc`). Так же собирается и экспортируется мапкит для мяк/навигатора и создается ревью на обновление. После завершения релизный процесс ставится на паузу.
3. **Тестирование**. Выполняется тестирование собранных приложений. Данная стадия не имеет отображения в CI и выполняется полностью командой тестировщиков.
4. **Экспорт артефактов**. На этой стадии собираются и загружаются в artifactory/cocoapods все конфигурации мапкитов, после чего релиз считается завершенным. Данную стадию необходимо запускать вручную после завершения тестирования (см. [Экспорт артефактов](#artifacts-export)).


## Создание нового релиза и релизной ветки
1. Открыть [релизы мапкита в CI](https://a.yandex-team.ru/projects/maps-core-mobile-arcadia-ci/ci/releases/timeline?dir=maps%2Fmobile&id=release-all).
2. Нажать `Run release`. В появившемся окне снова нажать `Run release`. Новая релизная ветка появится слева в списке после обновления страницы.


## Создание хотфикса
1. Найти и выбрать нужную релизную ветку в [списке "Release all mapkits" слева](https://a.yandex-team.ru/projects/maps-core-mobile-arcadia-ci/ci/releases/timeline?dir=maps%2Fmobile&id=release-all) 
ЛИБО перейти по ссылке `Release branch in CI` из релизного тикета.
2. Нажать `Run release`. В появившемся окне снова нажать `Run release`.

{% note warning %}

Запуск хотфикса отменяет предыдущий хотфикс/релиз в данной ветке, если для него не был запущен экспорт. Если экспорт артефактов все же требуется, то его нужно запустить ДО создания нового хотфикса.

{% endnote %}

## Экспорт артефактов после завершения тестирования {#artifacts-export}
1. Найти и выбрать нужную релизную ветку в [списке "Release all mapkits" слева](https://a.yandex-team.ru/projects/maps-core-mobile-arcadia-ci/ci/releases/timeline?dir=maps%2Fmobile&id=release-all), открыть последний релиз (ссылка `Release all mapkits #X.Y`) 
ЛИБО перейти по ссылке `Release in CI` из комментария от робота в релизном тикете.

2. Пролистать граф сборки вправо до задачи `Start export`, нажать play
    ![release-gandalf](images/release_gandalf.png)

## Черри-пик в релизную ветку

### Через UI арканума

Из релизного тикета перейти по ссылке `Release branch in CI`, нажать кнопку `Cherry pick` справа сверху, выбрать нужный коммит, запустить.

### Через `arc`

https://docs.yandex-team.ru/devtools/src/arc/branches#kak-sdelat-hot-fiks-v-reliznuyu-vetku

https://docs.yandex-team.ru/devtools/src/arc/branches#kak-perenesti-hot-fiks-iz-tranka-v-reliznuyu-vetku

Имя релизной ветки указано в релизном тикете в строчке `arc checkout releases/maps/mobile/mapkit-release-....`.
На текущий момент прямой push в релизную ветку запрещён. Возможно мы уберем это ограничение в дальнейшем.
