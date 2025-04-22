# Запросы статистики списаний

Иногда нужно посчитать точные суммы списаний за какой-то продукт, период, у какого-то клиента и прочее. 
Данный гайд содержит готовые запросы статистики списаний в YT и MySQL.

## Запросы в YT

- [Статистика сумм списаний с разбиением по дням и именам продуктов](https://yql.yandex-team.ru/Operations/YbyHNwVK8AskqRu52oEoKzZypzopaZ3ppXem-ejJX7A=)
- [Статистика сумм списаний с разбиением по дням и типам услуги](https://yql.yandex-team.ru/Operations/YbyHfy3DcA_PidQvzkvgftaNcehby-hZdk18wdTq6Ks=)
- [Статистика сумм списаний с разбиением по дням](https://yql.yandex-team.ru/Operations/YbyJrC3DcA_Pide5YyOb4JhCwjh4aWFg_Bekt_AVcZw=)
- [Статистика сумм списаний с разбиением по дням за указанный продукт](https://yql.yandex-team.ru/Operations/YbyNLdJwbA74bdk4jcf02hU000qgnVzjCa2Z3LicTco=)
- [Статистика сумм списаний с разбиением по дням за указанный заказ клиента](https://yql.yandex-team.ru/Operations/YcENj1Z1OyxB3xUqtKZrVmo7pslDbJ5a8PPSLWHEgS4=)
- [Статистика сумм списаний с разбиением по месяцам и именам продуктов](https://yql.yandex-team.ru/Operations/YcAsYS3DcA_PjxajGKCcvTxYD-jR4BMfSqQPgV9b2R8=)

## Запросы в MySQL

Запросы в MySQL полезны только в случае необходимости посчитать статистику быстрее, чем она будет считаться в YT. 
Во всех остальных случаях статистику стоит считать по YT.

Однако, с запросами в mysql нужно быть аккуратным -- не стоит их считать на большом количестве дней.

#### Статистика сумм списаний с разбиением по дням

<details>
<summary>Запрос</summary>
<p>

```sql
select day(timestamp), sum(amount), count(*) 
from order_transaction
where timestamp > '2021-11-20' 
  and timestamp < '2021-11-25' 
  and type = 2
group by day(timestamp);
```

</p>
</details> 

#### Cтатистика сумм списаний с разбиением по дням за указанный заказ клиента

<details>
<summary>Запрос</summary>
<p>

```sql
select day(timestamp), sum(amount), count(*) 
from order_transaction
where timestamp > '2021-11-10' 
  and timestamp < '2021-11-17'
  and type = 2
  and order_id = 47318
group by day(timestamp);
```

</p>
</details> 

#### Статистика сумм списаний с разбиением по месяцам

<details>
<summary>Запрос</summary>
<p>

```sql
select year(timestamp), month(timestamp), sum(amount), count(*)
from order_transaction
where timestamp > '2021-10' 
  and timestamp < '2021-12'
  and type = 2
group by year(timestamp), month(timestamp);
```

</p>
</details> 
