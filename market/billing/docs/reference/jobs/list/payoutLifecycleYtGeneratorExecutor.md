# payoutLifecycleYtGeneratorExecutor

### Код

[джоба payoutLifecycleYtGeneratorExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/report/payout/PayoutLifecycleYtGeneratorExecutor.java)


### Роль в работе продукта/подсистемы

Выгружает в YT данные о пэйаутах.


### Датафлоу

Читает из кучи табличек на YT. См. [пример запроса](https://yql.yandex-team.ru/Operations/YrmtiK5OD_RqKWqREi9JxIGED8bnANyKB-T9PprRV1k=)

Пишет в
`//home/market/production/billing/payout-stat/order-lifecycle/DATE`


### Способы наблюдения за текущим состоянием

- Juggler-проверки:
  tms-18


### Какая функциональность пострадает от отказа джобы




### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Елена Большакова](https://staff.yandex-team.ru/lena-san) <br/>

### Желательное время исправления в случае поломки
Несколько дней



### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

