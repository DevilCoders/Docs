---
title: Взаимодействия Я.Путешествия <> Биллинг <> OEBS
---
## Общее описание

Сервис выгружает строчки платежей в табличку в YT в формате, который предлагает Рома вот [тут](https://st.yandex-team.ru/BALANCE-34552#5ede40ad976bd04e0fe2260c).
Биллинг регулярно забирает эти данные и преобразует их внутри в тразанкции OEBS.
Преобразование происходит по правилам, которые опираются на `service_id`, `transaction_type`, `payment_type`, `paysys_type_cc`.
В том числе логика, на стороне биллинга относит сумму `amount` в `amount`, `amount_fee`, `yandex_reward`.

Список возможных значений для `payment_type` (в текущий момент) - **используется Биллингом для формирования актов и разметки платежей**:

**name** | **description (Ж/Д)** | **description (Отели)**
:--- | :--- | :---
cost            | Стоимость билета ЖД             | Услуга проживания в отеле   
reward          | Сбор Яндекса за ЖД билет        | АВ Яндекса за продажу отеля 
cost_insurance  | Стоимость страховки             | - (нет в договоре)          
reward_insurance| АВ за оформление страховки      | - (нет в договоре)          
fee             | Сбор ИМ за оформление и возврат | - (не применимо)            


Список возможных значений для `paysys_type_cc` (в текущий момент) - **используется для ОЕБС, чтобы выделить строчки в отчете агента и для отнесения строчек на нужные счета в бухгалтерии**:

**name** | **description (Ж/Д)** | **description (Отели)**
:--- | :--- | :---
sberbank        | деньги, принятые от пользователя за билет и наш сбор          | - ???           
insurance       | деньги, принятые от пользователя за страховку                 | - (не применимо)
yandex          | расходная часть (мы платим из этих денег сбор за оформление ) | - (не применимо)
yamoney         | не применимо                                                  | деньги, принятые с пользователя за бронирование отеля

## Маппинг внутри Биллинга

При этом логика маппинга из транзакций сервиса (stx) в транзакции OEBS (otx) может быть представлена следующим образом

```
otx.TRANSACTION_TYPE = stx.transaction_type
otx.PAYSYS_TYPE_CC = stx.paysys_type_cc
otx.PAYMENT_TYPE = stx.payment_type
otx.SERVICE_ID = stx.service_id

-- SERVICE_ID = 171

if( stx.SERVICE_ID == 171) {
	if( stx.paysys_type_cc == 'sberbank' && stx.payment_type == 'reward') {
	    otx.INTERNAL = 1 // не экспортируется в OEBS. наш сбор не попадает таким образом в отчет агента
	}
	else if( stx.paysys_type_cc == 'insurance' && stx.payment_type == 'reward_insurance') {
		otx.YANDEX_REWARD = stx.amount
	}
	else if( stx.paysys_type_cc == 'yandex' && stx.payment_type == 'fee' ) {
	    otx.AMOUNT_FEE = stx.amount
	}
	else {
	    otx.AMOUNT = stx.amount
	}
}

-- SERVICE_ID = 641

if( stx.SERVICE_ID == 641) {
	if( stx.paysys_type_cc == 'yamoney' && stx.payment_type == 'reward') {
		otx.YANDEX_REWARD = stx.amount
	}
	else {
	    otx.AMOUNT = stx.amount
	}
}
```

С учетом вышеизложенного суммы в договорах тогда можно представить следующим образом.

## Суммы для документов выраженные в терминах SQL поверх транзакций сервиса

### Service_id == 171: Ж/Д

#### Отчет агента

[Пример](https://yandexteam-my.sharepoint.com/:b:/g/personal/sandello_yandex-team_ru/EbSHS1rMEQ9Fm0M4Ve0P9YgBzIqUgTV6NRTHaxS4TAEdeg?e=abKa8S)

**Стоимость Электронных билетов**

```sql
SELECT SUM(value) FROM billing_transactions 
WHERE dt >= :period_start AND dt <= :period_end 
AND paysys_type_cc = 'sberbank' 
AND transaction_type = 'payment'
AND payment_type = 'cost'
```
￼
**Получено от пользователей в счет заключенных договоров согласно ДС 2 к договору** (страховка)

```sql
SELECT 
SUM(
   CASE WHEN transaction_type = 'payment' THEN value ELSE -value END
) 
FROM billing_transactions 
WHERE dt >= :period_start AND dt <= :period_end 
AND paysys_type_cc = 'insurance' 
```

**Возвращено платежей Пользователям**

```sql
SELECT SUM(value) FROM billing_transactions 
WHERE dt >= :period_start AND dt <= :period_end 
AND paysys_type_cc = 'sberbank' 
AND transaction_type = 'refund'
AND payment_type = 'cost'
```
￼
**Аванс за услуги Принципала**

```sql
SELECT SUM(value) FROM billing_transactions 
WHERE dt >= :period_start AND dt <= :period_end 
AND paysys_type_cc = 'yandex'
AND payment_type = 'fee'
```
￼
**Подлежит удержанию Агентом / Возвраты платежей Пользователей**

```sql
SELECT SUM(value) FROM billing_transactions 
WHERE dt >= :period_start AND dt <= :period_end 
AND paysys_type_cc = 'sberbank' 
AND transaction_type = 'refund'
AND payment_type = 'cost'
```

**Перечислено Агентом на счет Принципала** (это и есть депозит) 
Вычисляется автоматом, как сумма всех выплат в сторону партнера минус наши удержания.

#### Акт

[Пример](https://yandexteam-my.sharepoint.com/:b:/g/personal/sandello_yandex-team_ru/EfohGPeSdWtCitJm1BmzehwB-jXUKY9wAnS09UDgpXsy6Q?e=8mry5w)

```
Услуги по привлечению Клиентов для оформления Договоров страхования и 64 902,50 формирования Страховых полисов за/в май/е 2020 года
  Итого: ...
  Итого НДС: ...
  Всего по акту: ...
```

```sql
SELECT 
SUM(
   CASE WHEN transaction_type = 'payment' THEN value ELSE -value END
) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'insurance' 
AND payment_type = 'reward_insurance'
```

### Service_id == 641: Отели

#### Отчета агента (для TL/Bnovo-отелей)

[Пример](https://yandexteam-my.sharepoint.com/:b:/g/personal/sandello_yandex-team_ru/EZVlRfmOhtFNklNxcM_vakkBLRjshB9A-R7Qu1pItzhfOw?e=WphJfn)

**Получено от Пользователей в адрес Принципала**

```sql
SELECT 
SUM(value) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'yamoney'
AND transaction_type = 'payment'
```

**Возвращено платежей Пользователям**

```sql
SELECT 
SUM(value) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'yamoney'
AND transaction_type = 'refund'
```

**Возвраты платежей Пользователей**

```sql
SELECT 
SUM(value) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'yamoney'
AND transaction_type = 'refund'
```

**Вознаграждение Яндекса**

```sql
SELECT 
SUM(
   CASE WHEN transaction_type = 'payment' THEN value ELSE -value END
) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'yamoney' 
AND payment_type = 'reward'
```

**Перечислено Яндексом на счет Принципала**

Сумма расчитывается автоматом, как фактическая сумма денег, которые были перечислены принципалу.

#### Акт о выполненных поручениях (для TL/Bnovo-отелей)

[Акт](https://yandexteam-my.sharepoint.com/:b:/g/personal/sandello_yandex-team_ru/EZVlRfmOhtFNklNxcM_vakkBLRjshB9A-R7Qu1pItzhfOw?e=WphJfn)

```sql
SELECT 
SUM(
   CASE WHEN transaction_type = 'payment' THEN value ELSE -value END
) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'yamoney' 
AND payment_type = 'reward'
```

#### Работа выплат на стороне OEBS, и формирование актов

1. Для ЖД строчки из YT доезжая до oebs означают, что должна произойти выплата, как и в случае отелей (cost, insurance_cost, fee как раз эти суммы выплачиваются ИМ каждый день)
2. UpdatePaymentDt как и в случае отелей говорит, что данная строчка должна попасть в акт

## Промокоды (UPD 2020-07-30)

### Описание механизма

Промокоды - механизм предоставления скидок пользователю на сумму промокода. На начальном этапе запускаем промокоды для продажи отелей.
Схема работы отельных продаж подразумевает, что у нас есть договор с отелем. В рамках этого договора мы берем с пользователя деньги, оказываем пользователю услугу - делаем бронь в отеле, за которую должны перечислить деньги, удержав свое агентское вознаграждение. При использовании промокодов часть денег к перечислению в отель идет не из тех денег, что мы приняли от пользователя, а средств со счета собственных расходов сервиса.
Для учета в бухгалтерии деньги, выплачиваем партнеру в результате применения промокода должны попасть на **44 счет**
В акте деньги, выплаченные из собственных средств никак не фигурируют
В отчете агента деньги принятые от пользователя должны суммироваться с собственными расходами.

### Возможная реализация в биллинге и OEBS

Выделяем промокод отдельной строкой со своим `paysys_type_cc`.
В OEBS корректируются запросы для формирования отчета агента для учета нового `paysys_type_cc`

#### Было

**Получено от Пользователей в адрес Принципала**

```sql
SELECT 
SUM(value) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND paysys_type_cc = 'yamoney'
AND transaction_type = 'payment'
```

#### Стало

**Получено от Пользователей в адрес Принципала**

```sql
SELECT 
SUM(value) 
FROM billing_transactions 
WHERE update_dt >= :period_start AND update_dt <= :period_end 
AND (paysys_type_cc = 'yamoney' OR paysys_type_cc = 'promocode')
AND transaction_type = 'payment'
```
