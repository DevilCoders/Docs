## ExportAdvqHitsJob

### Продукт/подсистема

Изначально делалось для "Мастера кампаний" aka "Универсальные кампании" aka "UC" (`campaigns.source == 'uac'`), но возможно прорасло еще куда-нибудь.


### Роль в работе продукта/подсистемы

Сохраняет в MySQL прогноз показов на поиске по регионам и устройствам без учета ключевых фраз для отображения в интерфейсе.


### Датафлоу

- Читаем из [hahn.//home/advq/advq/normal/rus/weeklyhits](https://yt.yandex-team.ru/hahn/navigation?path=//home/advq/advq/normal/rus/weeklyhits) данные по всем регионам.
- Обрабатываем.
- Пишем в [ppcdict.advq_hits](https://direct-dev.yandex-team.ru/db/ppcdict/tables/advq_hits.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ExportAdvqHitsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/short/59hU8hoT3nx7Uk) (не забудьте исправить даты!)
- Время обновления самой старой записи: `select min(last_update) from advq_hits;`

### Какая функциональность пострадает от отказа джобы

Прогноз охвата для UC станет устаревшим.


### Как пользователи (или команда) заметят проблему и через какое время

- Пользователи - никак.
- Команда может случайно увидеть старый `last_update` в таблице [ppcdict.advq_hits](https://direct-dev.yandex-team.ru/db/ppcdict/tables/advq_hits.html).


### Контакты разработчиков и менеджеров

Разработчики: [Игорь Гердлер](https://staff.yandex-team.ru/gerdler), [Сергей Димитров](https://staff.yandex-team.ru/dimitrovsd)


### Желательное время исправления в случае поломки

3-4 дня


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Отсутствуют.


### Дополнительно: тонкости и подводные камни

Таблица хранится только в SAS, поэтому если ДЦ отключен - джоба простаивает (но не падает и никак о поломке не сообщает).
