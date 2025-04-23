## PopulateSuggestConversionPriceDynTableJob

### Продукт/подсистема

Рекомендации цены конверсии для пользователей, у которых настроена оплата за конверсию.

### Роль в работе продукта/подсистемы

Позволяет импортировать актуальную таблицу со средней ценой за конверсию из автобюджета.

### Датафлоу

[Исходные таблицы](https://yt.yandex-team.ru/hahn/navigation?path=//home/ads/cpa_autobudget/scripts/suggest_conversion_price)
Таблица с данными о средней цене за конверсию (в фишках) по типу атрибуции, категории товара, типу цели и региону.
Хранится в виде последовательных версий статических таблиц, причем новая появляется каждый день.
Для расчета значений используются данные за прошлые 7 дней, не считая текущий. </br>
[Итоговые таблицы](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/direct/import/cpa/suggest_conversion_price)
Данные пишутся в [реплицируемую таблицу](https://yt.yandex-team.ru/docs/description/dynamic_tables/replicated_dynamic_tables) на кластере `markov`,
затем прорастают в реплики на кластерах`seneca-sas`, `seneca-vla`, `seneca-man`.

- Поиск наиболее актуальной таблицы (с данными за прошлые 7 дней)
- Импорт новых значений

Джоба запускается каждый час. После успешного запуска обновляем проперти `last_successful_suggest_conversion_price_update_date`
Если таблица уже была успешно обновлена сегодня, то не пытается импортировать данные.

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.PopulateSuggestConversionPriceDynTableJob.working.production&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'*25PopulateSuggestConversionPriceDynTableJob*25)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Актуальность и точность рекомендованных стоимостей конверсий.

### Как пользователи (или команда) заметят проблему и через какое время

Могут заметить расхождения рекомендуемой цены и реальности. Если джоба в какой-то момент все данные или большую их часть,
то пропадут рекомендации целей без [статистики](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/yabs/stat/DirectGridGoalsStat)

### Контакты разработчиков и менеджеров

Разработчики: [Нина Жевтяк](https://staff.yandex-team.ru/ninazhevtyak), [Сергей Дмитриев](https://staff.yandex-team.ru/ssdmitriev) <br/>
Менеджеры: [Антон Огай](https://staff.yandex-team.ru/aogay)

### Желательное время исправления в случае поломки

Около недели. Данные в таблице будут не самые актуальные, но это не мешает их использовать.

### Способы регулирования работы джобы

- ppc-property `populate_suggest_conversion_price_dyn_table_job_enabled` - для включения/выключения джобы
- ppc-property `last_successful_suggest_conversion_price_update_date` - хранит дату последнего успешного обновления таблицы,
  чтобы обновлять таблицу единожды в день

### Известные причины поломок

-

### Дополнительно: тонкости и подводные камни

-
