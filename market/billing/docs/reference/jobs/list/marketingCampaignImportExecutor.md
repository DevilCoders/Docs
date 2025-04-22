# marketingCampaignImportExecutor

### Код
Основной код: [класс](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/marketing/MarketingCampaignImportExecutor.java),
[сервис](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/marketing/MarketingCampaignImportService.java),
[дао](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/marketing/MarketingCampaignDao.java),
[дао в YT](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/marketing/MarketingCampaignYtDao.java),


### Продукт/подсистема
Биллинг маркетинговых услуг. БМУ



### Роль в работе продукта/подсистемы
Импортирует данные о маркетинговых кампаниях



### Датафлоу
Раз в сутки забирает данные из таблиц на YT [marketing_campaigns_billing](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mbi/dictionaries/marketing_campaigns_billing/latest)
и записывает их в соответствующую таблицу `market_billing.marketing_campaign`.
Если у компании меняются данные, то изменения вносятся только если компания компенсационная и бюджет и\или дата завершения кампании увеличились.
См. подробнее [код](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/marketing/MarketingCampaignImportService.java?#L123)



### Способы наблюдения за текущим состоянием
_впиши актуальные ссылки_
- Juggler-проверки:<https://juggler.yandex-team.ru/check_details/?host=market-billing&service=marketingCampaignImportExecutor&query=&last=1DAY>
- Логи


### Какая функциональность пострадает от отказа джобы
Перестанут импортировать кампании -> перестанет работать биллинг -> теряем деньги



### Как пользователи (или команда) заметят проблему и через какое время
Мониторинг



### Контакты разработчиков и менеджеров

Разработчики: [Андрей Иванов](https://staff.yandex-team.ru/prof) <br/>


### Желательное время исправления в случае поломки
Неделя



### Способы регулирования работы джобы
Env-переменная `market.billing.marketing-campaigns.import-start-date` - дата с которой импортируют данне



### Известные причины поломок
Не доехала таблица на YT



### Дополнительно: тонкости и подводные камни
Джоба успешно выполняется строго раз в сутки. На выполнение дается полчаса. См. [аннотацию](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/marketing/MarketingCampaignImportExecutor.java?#L17)
