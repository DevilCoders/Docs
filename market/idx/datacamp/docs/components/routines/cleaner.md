# Сборщик мусора (datacamp_cleaner)

Удаления данных из офферного хранилища делится на две стадии:
- оффер помечается удаленным: продолжает храниться во внутренних таблицах, но не доступен в ручках stroller и выгрузках
- оффер окончательно удаляется из внутренних таблиц

**Важно** отличать понятия "помеченные удаленными" и "удаленные из таблицы".

#### Разметка

Чтобы пометить оффер удаленным, нужно установить признак [removed](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=8247635&blame=true#L221). Каждая часть united-оффер помечается удаленной отдельно.

Если вы хотите получать события об удалени офферов (или части офферов) из хранилища, достаточно подписаться на поле removed.

В stroller есть упрощенный интерфейс удаления с дополнительными проверками (наличие стока на FF-складе и пр.): можно удалять как [весь united-оффер](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#udalenie-bazovogo-offera), так и отдельные [сервисные части](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#udalenie-servisnogo-offera).

#### Сборщик мусора

Периодически запускается [задача](https://sandbox.yandex-team.ru/schedulers?tags=ROUTINES-DATACAMPCLEANER) очистки мусора в хранилище, в соответствии со [стратегиями](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/RemoveStrategy.proto#L10). Например, *из таблиц удаляются* офферы, помеченные удаленными более часа назад. Или еще пример: базовые офферы *помечаются удаленными*, если в течение суток (с момента создания базового оффера) не было создано ни одной сервисной части.

Данные об удаленных офферах, в соответствии со стратегиями, хранятся в YT, в директории [trash](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/trash). На данный момент хранится [5 последних запусков](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/lib/cleaner.py?rev=r8239066#L54). В таблицах basic, service, actual хранится информация о применении стратегий удаления к соответствующим частям оффера. В таблице ware_md5_duplicates хранится информация об [офферах-дубликатах в соответствии с контентом](https://yql.yandex-team.ru/Operations/YL8ZwRJKfZYMqKDRda0JB6mQsQ1p_0ZOFMNslHXI4aI=).

Сборщик мусора оснащен ручкой [clean](https://docs.yandex-team.ru/market-datacamp/support/admin#post-clean), которую можно использовать в двух режимах:
- для запуска сборщика мусора в обход расписания
- для удаления всех офферов магазина из таблиц. В этом режиме ручка защищена tvm.

#### Диагностика

- Поиск по [истории автоматического удаления](https://yql.yandex-team.ru/Operations/YVq2VxJKfZcFiXx1pcA5m2idQLkMjOjlvXAz9eRId6I=)
- Поиск по [истории ручного удаления](https://yql.yandex-team.ru/Operations/YWP38AVK8HYxUZ6f_JUHLkK_SidF1tvCxFoGU07DwuY=)
- Поиск по [стратегии автоматического удаления](https://yql.yandex-team.ru/Operations/Yg9jktJwbE55TKWFwaTQEUur9K1ix3v47n_Se9hAUoc=)

#### Метрики

- [Количество удалённых офферов с группировкой по стратегиям и таблицам](https://nda.ya.ru/t/N6hf23E159pMVg)

