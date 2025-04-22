# Компоненты Маркета для бизнеса

- [Очередь](https://st.yandex-team.ru/MFBDEV) задач
- [ABC-сервис](https://abc.yandex-team.ru/services/marketb2bclients/)
- [Сервис в Y.Deploy](https://yd.yandex-team.ru/projects/market-b2b-clients)
- PGaaS [прод](https://yc.yandex-team.ru/folders/akugt7rrckrcb029but5/managed-postgresql/cluster/mdb1dket7g6lnokgk743?section=overview) и
  [тестинг](https://yc.yandex-team.ru/folders/akugt7rrckrcb029but5/managed-postgresql/cluster/mdb97cptpatjminge898?section=overview)
- S3 [прод](https://yc.yandex-team.ru/folders/akut3gutno9l38p0v92s/storage/buckets/payment-invoices) и
  [тестинг](https://yc.yandex-team.ru/folders/akut3gutno9l38p0v92s/storage/buckets/payment-invoices-tst)
- [Графики](https://grafana.yandex-team.ru/d/aERPEm57k/market-marketb2bclients-auto-graph?orgId=1)

## Почтовые ящики @business.market.yandex.ru

Логины и пароли в [секретнице](https://yav.yandex-team.ru/?tags=market-b2b).

Администрирование ящиков через [Яндекс360](https://admin.yandex.ru)
* пользователь a.business.market@yandex.ru
* выбирать организацию где 4 пользователя

Для писем из триггерной платформы **LILICRM** заведены ящики
* noreply@business.market.yandex.ru - обратный адрес для писем черного маркета
* bounce@business.market.yandex.ru - отчеты рассылятора
* fbl@business.market.yandex.ru - отчеты рассылятора

## Таблица попавших под санкции

Для блокировки продаж контрагентам под санкциями раз в час вычитываем таблицу контрагентов под санкциями.
Таблица расположена в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/b2b/sanctions_list/spark_info_sanctions_check).

Обновление таблицы производится роботом раз в час из данных Такси. Подвешено [задание](https://sandbox.yandex-team.ru/scheduler/705447/view) для %%robot-market-b2b@%%.
