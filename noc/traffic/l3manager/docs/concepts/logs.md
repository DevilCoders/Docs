# Логи и мониторинг нагрузки

## Логи доступности {#logs}

L3 manager регулярно [проверяет доступность рилов](checks.md) вашего сервиса и хранит результаты проверки в [YT](https://yt.yandex-team.ru/).

Чтобы получить результаты проверок, используйте YQL-запрос:
```
USE hahn;
$format = DateTime::Format("%Y-%m-%d %H:%M:%S %Z");
SELECT 
    $format(DateTime::FromSeconds(Unwrap(CAST(unixtime AS Uint32)))) as time,
    msg,
    vs, vs_port,
    rs, rs_port
FROM
    LIKE("//logs/slb-keepalived-log/stream/5min","2020-06-05T18%")
WHERE
    rs='2a02:6b8:b000:504:202:c9ff:fef0:3ad1'
ORDER BY time DESC;
```

Этот запрос выведет все события по рилу `2a02:6b8:b000:504:202:c9ff:fef0:3ad1` за 05 июня в 18 часов.

Логи за все закончившиеся сутки доступны в виде таблиц [slb-keepalived-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//logs/slb-keepalived-log/1d). Чтобы получить данные логи, укажите необходимую вам таблицу в поле FROM.

Для удобства получения логов существует python-скрипт [slb-yql-query.py](https://github.yandex-team.ru/ezhichek/public/blob/master/scripts/slb-yql-query.py), который самостоятельно отправляет запросы в YQL и выводит данные в виде таблицы.

Для работы скрипта:
1. Создайте YQL-токен на странице [https://yql.yandex-team.ru/?settings_mode=token](https://yql.yandex-team.ru/?settings_mode=token).
1. Экспортируйте значение токена в переменную `export YQL_TOKEN=<значение токена>`.
1. Поставьте пакет `pip install -i https://pypi.yandex-team.ru/simple/ yql`.

## Графики мониторинга нагрузки {#grafs}

При помощи сервиса [Grafana](https://grafana.yandex-team.ru) вы можете строить графики с трафиком вашего сервиса.

Чтобы создать новый график:

1. В Grafana нажмите кнопку **Home**→**New dashboard**→**Graph**.
1. Измените название дашборда и сохраните изменения кнопкой ![image](../_assets/grafana-save.png).
1. Перейдите к редактированию графика, кликнув по названию и нажав **Edit**.
1. На вкладке **Metrics** выберите **Data-source**`ps-mg`.
1. Нажмите кнопку **Add Quiery**.
1. В поле **Series** укажите источники данных в следующем формате:
    
    ```
    one_min.l3_balancers.<балансер>.exec.vs_metrics.<сервис>.<порт>.<протокол>.<метрика>
    ```
    
    Параметры:
    
    #### Балансер
    FQDN балансера, в котором все точки (`.`) заменены нижним подчеркиванием (`_`). Если необходимо получать данные со всех балансеров, используйте символ `*`. Список существующих балансеров приведен в [L3 manager](https://l3.tt.yandex-team.ru/balancer).
    #### Сервис
    
    FQDN или IP-адрес вашего сервиса.
    
    Замените все точки (`.`) в FQDN или IP-адресе нижним подчеркиванием (`_`). Например, сервис `vins.alice.yandex.net` необходимо указывать как `vins_alice_yandex_net`.
    
    #### Порт
    Порт вашего сервиса, указанный на этапе [Настройки виртуального сервиса](config-settings.md#section_vxt_rlf_sfb).
    #### Протокол
    Протокол вашего сервиса, указанный на этапе [Настройки виртуального сервиса](config-settings.md#section_vxt_rlf_sfb).
    #### Метрика
    Тип отображаемой метрики. Возможные значения:
    - `conns` — соединения.
    - `inbytes` — входящие байты. Если необходимо просматривать информацию в битах, используйте scale(8).
    - `outbytes` — исходящие байты. Если необходимо просматривать информацию в битах, используйте scale(8).
    - `inpkts` — входящие пакеты.
    - `outpkts` — исходящие пакеты.
    
    Пример источника данных для всех подключений ко всем балансерам сервиса vins.alice.yandex.net:
    ```
    one_min.l3_balancers.*.exec.vs_metrics.vins_alice_yandex_net.*.*.conns
    ```
    
1. Сохраните изменения кнопкой ![image](../_assets/grafana-save.png).

