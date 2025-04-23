## ImportCryptaSegmentsJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Импортирует из YT в MySQL новые крипто-сегменты, чтобы в последствии их можно было выбрать и сохранить в ретаргетинге групп внутренней рекламы.


### Датафлоу

- Читает все данные из таблицы в YT: [//home/crypta/production/profiles/export/lab/segments](https://yt.yandex-team.ru/hahn/navigation?offsetValue=3194&path=//home/crypta/production/profiles/export/lab/segments), кластер HAHN.
- Вычисляет записи, которых не хватает в MySQL-таблице [ppc.crypta_goals](https://direct-dev.yandex-team.ru/db/ppcdict/tables/crypta_goals.html).
- Добавляет их в эту таблицу.

Джоба только добавляет записи, удаление или обновление не делается.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ImportCryptaSegmentsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/short/xxelbExa3nzdGY) (не забудьте исправить даты!)


### Какая функциональность пострадает от отказа джобы

Не получиться выбрать и сохранить новые сегменты для ретаргетинга групп внутренней рекламы в интерфейсе на странице создание/редактирование групп или при импорте из экселя.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователями являются наши маркетологи, и обычно они и являются заказчиками новых сегментов в крипте. Когда им понадобится для групп внутренней рекламы выбрать новые сегменты, они заметят их отсутствие.


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Захар Зибаров](https://staff.yandex-team.ru/zakhar) <br/>
Менеджеры: [Ваня Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

Зависит от необходимости использовать новые сегменты, которые не успели импортировать. В среднем починка ждет неделю, уточнить нужны ли срочно новые сегменты можно у маркетологов ([Марина Ежова](https://staff.yandex-team.ru/ezhova-m)).


### Способы регулирования работы джобы

- ppc-property `segments.last_import_date` — содержит дату генерации последней импортированной [YT-таблицы](https://yt.yandex-team.ru/hahn/navigation?offsetValue=3194&path=//home/crypta/production/profiles/export/lab/segments). Можно указать дату из прошлого, если джоба неверно импортировала данные, и после починки джобы их нужно заново импортировать. Дата сравнивается с атрибутом таблицы `generate_date`.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
