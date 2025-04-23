## AmoCRM

AmoCRM - crm-ка, которой пользуются выездные менеджеры, колл-центр, аккаунты и многие другие работники Яндекс.Аренды для ведения сделок с собственниками и жильцами.

### Полезные ссылки
- [Инстанс AmoCRM](https://yandexarenda.amocrm.ru/leads/pipeline/3245719/)
- [У кого просить креденшелы к AmoCRM](https://staff.yandex-team.ru/zhukovrv)
- [Документация по AmoCRM](https://www.amocrm.ru/developers/content/crm_platform/api-reference)

### Основные сущности AmoCRM
- [Воронки](https://www.amocrm.ru/developers/content/crm_platform/leads_pipelines) (пайплайны, pipelines) - контейнеры для сделок по их типу (например, [воронка по собственникам](https://yandexarenda.amocrm.ru/leads/pipeline/3245719/), [воронка по жильцам](https://yandexarenda.amocrm.ru/leads/pipeline/4045201)).
- [Сделки](https://www.amocrm.ru/developers/content/crm_platform/leads-api) (лиды, leads) - например, [одна сдача квартиры](https://yandexarenda.amocrm.ru/leads/detail/16234013) или [заселение одного жильца](https://yandexarenda.amocrm.ru/leads/detail/21168237), связаны с контактами в отношении "многие ко многим", всегда имеют некоторый статус выполнения.
- [Контакты](https://www.amocrm.ru/developers/content/crm_platform/contacts-api) (contacts) - люди (например, собственник или жилец), имеет ФИО и набор номеров телефона.
- [Кастомные поля](https://www.amocrm.ru/developers/content/crm_platform/custom-fields#cf-types) (custom fields) - параметры контактов и сделок, которые можно заводить, задавая тип и название; имеют `fieldId`, а enum-поля - ещё `enumId` для каждого enum-значения.
- [Юзеры](https://www.amocrm.ru/developers/content/crm_platform/users-api) (users) - пользователи AmoCRM (т. е. выездные менеджеры, колл-центр, аккаунты и другие).
- [Задачи](https://www.amocrm.ru/developers/content/crm_platform/tasks-api) (таски, tasks) - например, "позвонить собственнику", "проверить документы", привязываются к сделкам, ассайнятся на юзеров AmoCRM.
- [Заметки](https://www.amocrm.ru/developers/content/crm_platform/events-and-notes#notes-common-info) (notes) - текстовые примечания, пишутся в сделки и задачи.
- [События](https://www.amocrm.ru/developers/content/crm_platform/events-and-notes#events-list) (events) - эвенты об изменениях той или иной сущности (например, сделки).

### Воронки

Полный список воронок в Амо можно увидеть, наведя на "Сделки" в боковом меню Амо. Т. к. инстанс Амо - общий на прод и тестинг, там есть разделение на продовые и тестинговые воронки. В базу данных Амохаба [зеркалируются](https://docs.yandex-team.ru/realty/rent/amohub/amo-synchronization) сделки не из всех воронок, а только из четырёх.

Продовые воронки:
- [воронка по собственникам](https://yandexarenda.amocrm.ru/leads/pipeline/3245719) - заявки собственника на сдачу квартиры, requests pipeline;
- [воронка по жильцам](https://yandexarenda.amocrm.ru/leads/pipeline/4045201) - она же воронка по показам, заявки жильцов на заселение;
- [воронка КЦ](https://yandexarenda.amocrm.ru/leads/pipeline/3733723) - на каждый оффер Недвижимости создаётся сделка, в рамках неё сотрудник КЦ звонит собственнику и предлагает воспользоваться нашим сервисом;
- [воронка съездов](https://yandexarenda.amocrm.ru/leads/pipeline/4387657) - общение с жильцами и собственниками про съезд с квартиры.

Тестинговые воронки:
- [воронка по собственникам](https://yandexarenda.amocrm.ru/leads/pipeline/3721138);
- [воронка по жильцам](https://yandexarenda.amocrm.ru/leads/pipeline/4408051);
- [воронка КЦ](https://yandexarenda.amocrm.ru/leads/pipeline/3738658);
- [воронка съездов](https://yandexarenda.amocrm.ru/leads/pipeline/4986286).
