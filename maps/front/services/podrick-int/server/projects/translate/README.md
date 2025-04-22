# Создание тикета для переводчиков при релизе

При выкатке нового __тестинга__ хук выгружает переводы указанного проекта, находит ключи, переводы которых находятся в одном из статусе `requires_translation`, `expired` или `generated`, и создает для них тикет в очереди [TRANSLATE](https://st.yandex-team.ru/TRANSLATE). К тикету в наблюдатели также будут добавлены авторы непереведенных ключей.

## Адрес

`/translate`

## Методы

`POST`

## Параметры

* `followers` — список логинов через запятую, которые будут добавлены в наблюдатели к созданному тикету.
* `strict-followers` — добавлять в наблюдатели только людей из параметра `followers`. По умолчанию `false`.

Все остальные параметры передаются в [АПИ танкера](https://doc.yandex-team.ru/Tanker/api-reference/concepts/operations-translations.html#operations-translations__trans-download) для выгрузке переводов, поэтому документацию читайте там же. Используется ручка `/projects/export/tjson/`.

## Примеры

* `https://podrick.c.maps.yandex-team.ru/translate/?project-id=loris`
* `https://podrick.c.maps.yandex-team.ru/translate/?project-id=loris&branch-id=master`
* `https://podrick.c.maps.yandex-team.ru/translate/?project-id=loris&followers=sigorilla,hevil`
* `https://podrick.c.maps.yandex-team.ru/translate/?project-id=loris&followers=sigorilla&strict-followers`

## Backdoor

Вы можете использовать метод `GET` с дополнительным параметром `force-create-ticket` на __свой страх и риск__ для создания тикета без проверки хуков кондуктора.
