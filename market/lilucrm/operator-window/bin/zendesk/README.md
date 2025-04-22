# Загрузка тикетов из ZenDesk
Написано в рамках тикета [OCRM-1596](https://st.yandex-team.ru/OCRM-1596).

Установить зависимости:
```sh
make init
```

Запустить тесты:
```sh
make test
```

## Загрузить все тикеты с начала времён в `.out/pages`

### Вариант 1
С помощью ручки [/tickets.json](https://developer.zendesk.com/rest_api/docs/support/tickets).
Не устойчивый вариант. Каждый раз выгружается разное число тикетов.
```sh
./get-tickets.py
```
Можно спокойно перезапускать, уже загруженные и обработанные страницы игнорируются.
3805 страниц закачалось примерно в течение получаса.

### Вариант 2
С помощью ручки инкрементального экспорта [/incremental/tickets.json](https://developer.zendesk.com/rest_api/docs/support/incremental_export).
```sh
./import-tickets.py
```
Чтобы продолжить после остановки или дозагрузить свежие записи, надо передать новый таймстамп,
который можно достать из названия последней загруженной страницы.
```sh
./import-tickets.py $(./get-last-import-page-end-time.sh)
```
Вместе это заняло около 3.5 часов.
И эту часть нельзя сделать быстрее за счёт распараллеливания, из-за ограничения в 10 rpm на эту ручку.

## Загрузка комментариев
Пройтись по всем загруженным страницам и "обогатить" их комментариями, сохранив результаты в `.out/commented_pages`:
```sh
./get-comments.py
```
На том же объёме отработало примерно за 6 часов.
За прогрессом можно следить с помощью
```sh
./get-comments-progress.sh
```
Можно останавливать и перезапускать.
Загружаются только комментарии к тем файлам, для которых ещё нет обогащённого варианта.

## Объединение и разбивка
Слепить все комментарии в один большой файл в формате [Line-delimited JSON](http://jsonlines.org/): `.out/tickets.jsonl`,
а потом разбить его по каналам и брендам
(результаты сохраняются в файлы вида: `.out/tickets_$CHANNEL_$BRAND.jsonl`;
конкретные названия печатаются по ходу выполнения):
```sh
./join-tickets.sh
```
Работает около 5 минут.

Конвертировать `*.jsonl` файлы в `*.csv` и `*.xslx`, сложив их рядом с исходными:
```sh
./tickets-to-table.py
```
Тоже около 5 минут.

## Запаковать результат
```sh
./archive-out.sh
```
Получится архив вида `zendesk_tickets_yyyy-mm-dd.tgz` (например `zendesk_tickets_2019-07-23.tgz`),
где дата - это дата последних прочитанных тикетов (соотв. таймстам получается с помощью `./get-last-import-page-end-time.sh`).

Структура архива:
* `/zendesk_tickets`
  * `/pages/page_xxx_yyy.json` - "сырые" тикеты без комментариев - конвертированная страница со `start_time=xxx` ответа ручки `GET https://yandex-market.zendesk.com/api/v2/[incremental]/tickets.json`
  * `/commented_pages/page_xxx_yyy.json` - "сырые" тикеты с комментариями - страница `/pages/page_ddddd.json`, обогащённая комментариями из ручки `GET /api/v2/tickets/${ticket_id}/comments.json`
  * `/tickets.jsonl` - страницы `/commented_pages/page_ddddd.json` слепленные в один файл в формате [Line-delimited JSON](http://jsonlines.org/) - в каждой строчке файла один JSON объект, представляющий тикет с комментариями.
  * `/tickets_${channel}_${brand}.jsonl` - разбивка файла `/tickets.jsonl` по каналам и брендам
  * `/tickets*.{csv,xlsx}` - `*.jsonl` файлы, сконвертированные в табличный формат, со склеиванием `fields` и `comments`
`*.csv` и `*.xlsx` файлы все отсортированы по id тикета, а `*.jsonl` не сортировались

# Утилиты
`./get-tickets.sh` и `./import-tickets.sh` для непосредственного тестирования ручек
[/tickets.json](https://developer.zendesk.com/rest_api/docs/support/tickets)
и [/incremental/tickets.json](https://developer.zendesk.com/rest_api/docs/support/incremental_export)
соответственно.

Они внутри вызывают `./curl-zd.sh` - утилиту для вызова любых ручек
[ZenDesk API](https://developer.zendesk.com/rest_api/docs/support/introduction).

`./get-comments.sh` - аналогично, для тестирования ручки `/tickets/${ticket_id}/comments.json`

