# Маркет.Аналитика

[Swagger UI](https://analytics.tst.vs.market.yandex.net/swagger-ui.html)

Данные в стейте:
```js
{
    /**
     * Информация о балансе офертного вендора
     */
    balance: {
        actualBalance: number, // Текущий баланс вендора
        allowedSpendSum: number, // Сколько можно потратить с учётом замороженных средств
        datasourceId: number, // Идентификатор датасорца в CS-Billing
        nextMonthLackSum: number, // Недостаток денег на начало следующего месяца
        summaryCost: Object, // Суммарная цена по периодам (см. SummaryCost в свагере)
    },
}
```

#### GET `/vendors/<vendorId>/balance`

Возвращает информацию о балансе офертного вендора

##### Параметры
  - **vendorId** `<number>` - идентификатор вендора

##### Ответ
  - **vendorId** `<number>` - идентификатор вендора
  - **actualBalance** `<number>` - баланс услуги (в рублях)
  - **allowedSpendSum** `<number>` - сколько можно потратить с учётом замороженных средств
  - **datasourceId** `<number>` - идентификатор датасорца в CS-Billing
  - **nextMonthLackSum** `<number>` - недостаток денег на начало следующего месяца
  - **summaryCost** `<Object>` - суммарная цена по периодам (см. SummaryCost в свагере)
