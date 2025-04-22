# InstallmentReturnBillingExecutor

### Код

Основной код:

[класс InstallmentReturnBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentReturnBillingExecutor.kt)

[класс InstallmentReturnBillingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentReturnBillingService.kt)

[dao InstallmentReturnBillingDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentReturnBillingDao.kt)

### Продукт/подсистема


Синий биллинг возвратов рассрочки.


### Роль в работе продукта/подсистемы

Джоба биллит услугу отмены комиссии при оплате в рассрочку при возврате товара. Если товар рассрочки вернули в течение
30 дней с момента обилливания, то надо откатить комиссию по рассрочке.


### Датафлоу

Джоба работает через стандартный механизм биллинга услуг - processDaysUntilYesterday. Последовательно обрабатывает дни,
начиная со значения переменной в env [ENV_INSTALLMENT_RETURN_BILLING_START_DATE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentReturnBillingExecutor.kt#L29),
заканчивая вчерашним днем.

Алгоритм работы:
- получаем трантаймы за дату обилливания из таблицы [market_billing.order_return_trantimes](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_return_trantimes.sql)
- получаем данные из таблицы позиций возвратов [market_billing.order_return_item](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_return_item.sql)
- получаем список из order_item_id, которые не нужно биллить
- из полученных данных выше формируем обилленные значения
- зануляем данные в таблице с обиленными значениями [market_billing.installment_return_billed_amount](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/installment_return_billed_amount.sql)
- записываем обиленные значения в таблицу [market_billing.installment_return_billed_amount](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/installment_return_billed_amount.sql)


### Способы наблюдения за текущим состоянием


### Какая функциональность пострадает от отказа джобы

Не будет биллиться услуга отмены комиссии при оплате в рассрочку при возврате товара.

### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [rhrrd](https://staff.yandex-team.ru/rhrrd) <br/>

### Желательное время исправления в случае поломки

К закрытию месяца джоба должна отработать.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

