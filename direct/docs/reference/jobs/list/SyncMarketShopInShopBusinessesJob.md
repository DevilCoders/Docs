## SyncMarketShopInShopBusinessesJob


### Продукт/подсистема

Товарная реклама(Смарты, ДО, Фиды в ТГО).


### Роль в работе продукта/подсистемы

Выгружает информацию о бизнесе в маркетплейсе Маркета (урл фида и номер счетчика метрики) в таблицу `ppcdict.shop_in_shop_businesses`.


### Датафлоу

- Данные о бизнесе и фиде берутся из таблицы [//home/market/production/mstat/dictionaries/mbi/partner_biz_snapshot/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/partner_biz_snapshot/latest). Счетчики метрики берутся из таблицы [//home/market/production/mstat/dictionaries/mbi/business_metrika/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/business_metrika/latest).
- Результаты складываются в таблицу `ppcdict.shop_in_shop_businesses`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.SyncMarketShopInShopBusinessesJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/short/jZu1ppGF4scxNk)


### Какая функциональность пострадает от отказа джобы

Перестанут обновляться данные о бизнесах маркетплейса Маркета.


### Как пользователи (или команда) заметят проблему и через какое время

Будут появляться жалобы от клиентов, что бизнес существует в Маркете, но не определяется при создании товарной кампании.

### Контакты разработчиков и менеджеров

Разработчики: [Дмитрий Анощенков](https://staff.yandex-team.ru/dmitanosh) <br/>
Менеджеры: [Дмитрий Уляшев](https://staff.yandex-team.ru/ulyashevda)


### Желательное время исправления в случае поломки

Дни, т.к. поломка джобы не создаст для пользователей непреодолимых проблем. Но, по мере устаревания данных, пользователям придётся совершать больше действий для запуска рекламы.


### Способы регулирования работы джобы


### Известные причины поломок

Превышение количества бизнесов в выгрузке из yt указанного в джобе лимита.


### Дополнительно: тонкости и подводные камни
