# Скрипт по мониторингу частоты обновления источников

## Описание

Скрипт работает на уровне дирректорий в YT+по имени конкретной таблицы. Все настройки создаются на директорию (проект), но можно сделать так, что бы для каждой таблицы были свои настройки по SLA.

Сама морда отчета в DataLens лежит тут: https://datalens.yandex-team.ru/748ov2r0ddyaz-oklo-navigator-po-otchetam?tab=nz

Кубик мониторинга срабатывает каждые 10 минут. Мониторинга на срабатывание мониторинга нет :)

Что бы добаить дополнительный истоник для мониторинга, необходимо добавить следующий код (тут и далее `claim_sd` заменить на имя вашего проекта):

```yql
--claim_sd
$claim_sd_yt = ("//home/market/production/oklo/prod/claim_sd");
$claim_sd_name = ("claim_sd");
$claim_sd_type = ("prod");
$claim_sd_sla = (0.083);
$claim_sd = (
SELECT
    "home/market/production/oklo/prod/claim_sd/YT_JUDGE_DREDD_TTL" as Path,
    $claim_sd_name as Project_name,
    $claim_sd_type as Project_type,
    $claim_sd_sla as SLA_day,
    CurrentUtcDatetime() as Report_datetime,
UNION ALL
SELECT
    "home/market/production/oklo/prod/claim_sd/YT_JUDGE_DREDD_compensation" as Path,
    $claim_sd_name as Project_name,
    $claim_sd_type as Project_type,
    $claim_sd_sla as SLA_day,
    CurrentUtcDatetime() as Report_datetime,
UNION ALL
SELECT
    "home/market/production/oklo/prod/claim_sd/YT_JUDGE_DREDD_transactions_auto" as Path,
    $claim_sd_name as Project_name,
    $claim_sd_type as Project_type,
    $claim_sd_sla as SLA_day,
    CurrentUtcDatetime() as Report_datetime,
);
```

## Разбор скрипта (без деталей, только то что надо задавать руками)

### Переменные проекта

**ВАЖНО!** далее часть названий переменных `claim_sd` необходимо заменить на имя проекта, который необходимо добавить.

```yql
$claim_sd_yt = ("//home/market/production/oklo/prod/claim_sd");
$claim_sd_name = ("claim_sd");
$claim_sd_type = ("prod");
$claim_sd_sla = (0.083);
```

- В переменной `claim_sd_yt` указывается путь до таблиц, данные об изменении которых мы хотим собирать. Важно: 1 проект = 1 путь до таблиц. *Пример: //home/market/production/oklo/prod/claim_sd*
- `claim_sd_name` - тут задаем название проекта
- `claim_sd_type` - задаем тип проекта: продовый он или нет, а именно
  - *prod* - продакшен проект
  - *users* - все что лежит в папке user - по сути тест, может лежать как в паке users в старом OKLO так и в *//home/market/production/oklo/prod/users*
- `claim_sd_sla` - тут задаем наши ожидания (SLA), как часто должен обновляться источник, если он будет обновлять реже - будет красным гореть в мониторинге. Время измеряется днями. *Пример: если ожидаем, что источник работает каждые 12 часов, значит SLA = 1/12 = 0.5*

### Подключение таблиц

```yql
SELECT
    "home/market/production/oklo/prod/claim_sd/YT_JUDGE_DREDD_TTL" as Path,
    $claim_sd_name as Project_name,
    $claim_sd_type as Project_type,
    $claim_sd_sla as SLA_day,
    CurrentUtcDatetime() as Report_datetime,
UNION ALL
```

Далее идут блоки как пример выше, при этом 1 таблица = 1 блок. В блоке меняем только атрибут: `"home/market/production/oklo/prod/claim_sd/YT_JUDGE_DREDD_TTL" as Path,` - тут указываем путь до таблицы.

### Финалочка

```yql
--Вытягиваем атрибуты таблиц

$atributes = (
    SELECT * FROM $sub_atributes($CLAIMFF_yt) UNION ALL
    SELECT * FROM $sub_atributes($claim_sd_yt)
);

--Объединяем все в одну кучу
$main = (
    SELECT * FROM $claim_sd UNION ALL
    SELECT * FROM $CLAIMFF
);
```

Тут добавляем строчки, исходя из правила: 1 проект = 1 строка:
- `SELECT * FROM $sub_atributes($CLAIMFF_yt) UNION ALL` - тут указываем только переменную, которую объявляли ранее - путь до папки проекта
- `SELECT * FROM $claim_sd UNION ALL` - тут указываем переменную, в которой подключали таблицы в пункте выше

### PROFIT!!!
