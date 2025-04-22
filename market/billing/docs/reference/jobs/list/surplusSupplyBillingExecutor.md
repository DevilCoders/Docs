# SurplusSupplyBillingExecutor

### Код

Основной код:

[класс SurplusSupplyBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/surplus/SurplusSupplyBillingExecutor.java)

[класс SurplusSupplyBillingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/surplus/SurplusSupplyBillingService.java)

[dao SurplusSupplyBillingDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/surplus/SurplusSupplyBillingDao.java)

### Продукт/подсистема


Синий биллинг излишков в поставках.


### Роль в работе продукта/подсистемы

Джоба биллит услугу излишков в поставках товаров.


### Датафлоу

Джоба работает через стандартный механизм биллинга услуг - processDaysUntilYesterday. Последовательно обрабатывает дни,
начиная со значения переменной в env [ENV_START_DATE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/surplus/SurplusSupplyBillingExecutor.java#L18),
заканчивая вчерашним днем.

Алгоритм работы:
- получаем информацию по поставкам с излишками из таблиц [market_billing.fulfillment_supply_item](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/fulfillment_supply_item.sql) и
  [market_billing.fulfillment_supply](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/fulfillment_supply.sql), вместе с ВГХ.
- получаем список партнеров с промо-тарифами, которых не нужно биллить из таблицы [market_billing.supplier_promo_tariffs](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/supplier_promo_tariffs.sql)
- из полученных данных выше формируем обилленные значения с тарифами
- получаем список уже забранных в тлог данных и фильтруем по ним полученные новые поставки, игнорируя таким образом заново пришедшие финальные статусы
- зануляем данные в таблице с обиленными значениями [market_billing.surplus_supply_item_blld_mnt](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/surplus_supply_item_blld_mnt.sql)
 и записываем в нее значения


### Способы наблюдения за текущим состоянием
juggler-мониторинг [surplusSupplyBillingExecutor](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=surplusSupplyBillingExecutor&project=market-billing&last=1DAY)

### Какая функциональность пострадает от отказа джобы

Не будет биллиться услуга излишков в поставках

### Как пользователи (или команда) заметят проблему и через какое время
мониторинг, сразу



### Контакты разработчиков и менеджеров

Разработчики: [rhrrd](https://staff.yandex-team.ru/rhrrd) <br/>

### Желательное время исправления в случае поломки

К закрытию месяца джоба должна отработать.


### Способы регулирования работы джобы
env-переменная
[ENV_START_DATE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/surplus/SurplusSupplyBillingExecutor.java#L18) -
  с какой даты биллить.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
Могут несколько раз приходить финальные статусы. Если это происходит в последующих, после крайнего обилливания месяцах, то статус игнорируется.
