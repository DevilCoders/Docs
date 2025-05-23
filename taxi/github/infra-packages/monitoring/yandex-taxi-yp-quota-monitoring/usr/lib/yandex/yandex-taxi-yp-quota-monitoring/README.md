## Скрипт мониторинга квот YP для monrun.
При запуске получает конфиг порогов для clown'а, при которых будет блокироваться возможность добавления ресурсов, из сервиса конфигов. 
Если требуемого сервиса нет в полученном конфиге - пороги устанавливаются по умолчанию.
**config-файл**: _quota_monitor/config.py_:
```
[main]
Основные настройки скрипта.
solomon token: SOLOMON_OAUTH из taxi_secdist_file

[monrun]
Основные настройки monrun'а

[configs-service]
configs_taxi_url - сервис конфигов
clownductor_conf_name - конфиг Clownductor'а из которого берутся значения порогов. Если сервис не найден в конфиге - проставляются дефолтные значения из [defaults].tresholds

[solomon]
monitoring_interval_sec - интервал времени, за который берется среднее значение из Соломона
solomon_datetime_pattern - используемый формат времени в API Solomon'а

[projects]
Проекты, локации и метрики
services:
  name - имя метрики в Solomon'е
  treshold_rule - правило, по которому происходит мониторинг:
    dc - метрики проверяются по каждой локации
    total - проверяется только общая(суммарная) метрика. Т.е. если ресурсы есть хотя бы в одном ДЦ - будет приходить ОК
  result - формат выводимого сообщения:
    short - содержит:
      - имя проекта
      - ДЦ
      - метрика
      - ссылка на дашборд в графане
    extend - содержит:
      - имя проекта
      - ДЦ
      - метрика
      - название сенсора в Соломоне
      - quota
      - usage
      - значение, при котором сработал мониторинг
      - значение, при котором будет произведена блокировка
      - примерная оценка в % до блокировки
      - ссылка на дашборд в графане
  sence_delta - кастомный порог sence_delta из [defaults]. При отсутствии, берется дефолтный

[defaults]
  thresholds - значения порогов по умолчанию
    sence_delta - Запас для отправки сообщений. На это значение уменьшаются пороги полученные из сервиса конфигов или дефолтные пороги.
```
