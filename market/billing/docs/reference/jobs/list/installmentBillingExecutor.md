# InstallmentBillingExecutor

### Код

Основной код:

[класс InstallmentBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentBillingExecutor.java)

[класс InstallmentBillingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentBillingService.java)

[dao InstallmentBillingDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentBillingDao.java)

### Продукт/подсистема


Синий биллинг рассрочки.


### Роль в работе продукта/подсистемы

Джоба биллит услугу рассрочки при оплате товара.


### Датафлоу

Джоба работает через стандартный механизм биллинга услуг - processDaysUntilYesterday. Последовательно обрабатывает дни,
начиная со значения переменной в env [ENV_BILLING_START_DATE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentBillingExecutor.java#L17),
заканчивая вчерашним днем.

Алгоритм работы:
- получаем трантаймы за дату обилливания из таблицы [market_billing.order_trantimes](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_trantimes.sql)
- получаем список из order_item_id, которые нужно обиллить
- из полученных данных выше формируем обилленные значения
- зануляем данные в таблице с обиленными значениями [market_billing.installment_billed_amount](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/installment_billed_amount.sql)
 и записываем в нее значения


### Способы наблюдения за текущим состоянием


### Какая функциональность пострадает от отказа джобы

Не будет биллиться услуга оплаты товара рассрочкой

### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [rhrrd](https://staff.yandex-team.ru/rhrrd) <br/>

### Желательное время исправления в случае поломки

К закрытию месяца джоба должна отработать.


### Способы регулирования работы джобы
env-переменная
- [ENV_BILLING_STOP_ON_EXCEPTION](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentBillingExecutor.java#L18) -
Отвечает за то надо ли падать джобе при ошибке
- [ENV_BILLING_START_DATE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentBillingExecutor.java#L17) -
  с какой даты биллить.



### Известные причины поломок




### Дополнительно: тонкости и подводные камни

