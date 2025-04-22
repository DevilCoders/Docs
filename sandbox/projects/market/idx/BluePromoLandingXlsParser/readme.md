# Оглавление
2. [Общее описание](#general)
2. [Рантайм (Sandbox)](#sandbox)
3. [Мониторинги](#monitorings)
3. [Локальный запуск](#local)
3. [Релиз](#release)
4. [Мониторинги](#monitorings)
4. [Квоты](#quotas)

## Общее описание { #general }
Робот призван для регулярного автоматического обновления контента CMS страниц в случае обновления XLS файла в тикете акции для карусели промолэндингов

[Продуктовое описание](https://docs.yandex-team.ru/marketpromo/landing/)

Список обрабатываемых тикетов можно взять из фильтра в стартреке. Номер фильтра передаётся как параметр запуска шедулера `st_filter_id`

Слой бизнес логики хранится отдельно:
https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/promos/blue_promo_landing

## Рантайм { #sandbox }
Продовый шедулер sandbox https://sandbox.yandex-team.ru/scheduler/22164/view
Тестинг https://sandbox.yandex-team.ru/scheduler/21901/view

Робот идёт в Startrack API, вытягивает тикеты по фильтру.
Берёт каждый тикет, вытаскивает из него аттачменты.
Самый свежий xlsx аттачмент он парсит, валидирует.
Если есть ошибки валидации - пишет внятный комментарий в тикет.
Если ошибок нет - обновляет CMS и делает запись в YT в указанные кластера по указанным в конфигурации шедулера путям.

{% note alert %}

Сейчас запись в YT в проде сломана, но это не влияет на работу робота

{% endnote %}

## Локальный запуск {% local %}
1. Запустить сборку (`ya make`) из папки с бизнес логикой https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/promos/blue_promo_landing
3. Получить и сохранить [токен Startrack](https://wiki.yandex-team.ru/tracker/api/#avtorizacija)
4. Получаем и сохраняем [YT токен](https://yt.yandex-team.ru/docs/quickstart#how-to-get-oauth-token)
5. Можно пропустить и пользоваться [дефолтным фильтром](https://st.yandex-team.ru/issues/68116). Для целей тестирования создаём задачку в очереди BLUEACTION (пример BLUEACTION-235)
 и сохранённый фильтр так, чтобы подходил только один этот тикет (пример фильтра https://st.yandex-team.ru/issues/69728). Из урла фильтра запоминаем номерок (тут: 69728)
6. Из директории `bin/blue_promo_landing_xls_robot` выполнить (или без параметра `st-filter-id`):
```bash
export ST_TOKEN=AQAD-xxxxxxxxxxxxxxxxxxxxx

./blue_promo_landing_xls_robot --st-filter-id=69728
```
7. Экспериментируем, загружая разные файлы в тикет, меняя, пересобирая и запуская кодину локально. Путь на yt берётся из переменной `yt_output_path`

## Релизный процесс {% release %}
1. Запускаем сборку через `ya make` из папки сендбокса https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/market/idx/BluePromoLandingXlsParser/bin
2. Из этой папки запускаем `./market_blue_promo_landing_parse_xls upload --attr task_type=BLUE_PROMO_LANDING_XLS_PARSER`
3. В выводе команды ищем текст и переходим по урлу
`Uploading task #708001377 created: https://sandbox.yandex-team.ru/task/708001377`
4. Ждём некоторое время, там появится (после загрузки) строчка вида `Tasks binary. (1575690108)`, копируем чиселко
5. Заходим в [тестовый шедулер](https://sandbox.yandex-team.ru/scheduler/21901/view), жмякаем Edit, идём в Advanced, подменяем Tasks Resource на скопированный в прошлом пункте, сохраняем
6. Ждём некоторое время, когда скедулер подхватит и запустит наш бинарник, либо стартуем сами
7. Проверяем (на всякий случай) в свойствах запуска, что запустился именно новый бинарник (поле Task resource в таске запуска должно совпадать с нашим)
8. Проверяем результаты по логам, YT и т.п.
9. Обновляем продовый шедулер

## Мониторинги {% monitorings %}
Мониторинги работы тасок
https://arcanum.yandex-team.ru/arc_vcs/market/solo_monitorings/marketpromo/registry/alerts/sandbox/robot.py

## Квоты {% quotas %}
1. Ресурсы sandbox в квоте MARKETPROMO
https://sandbox.yandex-team.ru/admin/groups/MARKETPROMO/general
2. Ресурсы YT в квоте market-indexer-production
