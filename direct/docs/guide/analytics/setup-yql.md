# Настройка YQL

## Доступы
Для работы с большинством данных нужно настроить авторизацию.

Откройте настройки [YQL](https://yql.yandex-team.ru/):
нажмите на значок шестерёнки в левом нижнем углу.
Доступы настраиваются на табе **Auth**.


### к данным в YT { #access-yt }
Кликните по кнопке **Use my token in YT by default**.

Может открыться страница oauth.yandex-team.ru, на ней нужно будет разрешить доступ.


### к данным в кликхаусе Директа { #access-ppchouse }
Речь о кластере с логами: `ppchouse.yandex.net` (`ppchouse-cloud.direct.yandex.net`).  
Этот токен надо настроить например чтобы заработала кнопка `Open in YQL` в Logviewer. 

Откройте [секрет](https://yav.yandex-team.ru/secret/sec-01e9ghqghxz51aysamvmkw0qrj/explore/version/ver-01e9ghqgjabvn43p2h802m2td8)
с паролем от кликхауса, скопируйте значение.
При отсутствии доступа — пишите [mokeev@](https://staff.yandex-team.ru/mokeev), [ppalex@](https://staff.yandex-team.ru/ppalex).

В настройках YQL в разделе **Cluster tokens** нажмите кнопку **Add token**.
В открывшемся окне укажите:

- System: `ClickHouse`
- Type: `Custom`
- Name: `default_ppchouse`
- Token: `basic#yql_direct#вставьте_сюда_значение_секрета`

Нажмите **Add**.

Для проверки правильности настройки — попробуйте выполнить [запрос](https://yql.yandex-team.ru/Operations/Xut6lxpqvyAIWpIBDADSgI5NFMa3_OrKPF0a1JDizyY=).

Если не работает и возвращается ошибка "No authentication information found" перепроверьте, что правильно указали значение Token.

Для ТС кликхауса в YQL нет, в ТС можно ходить только так `direct-sql ts:ppchouse:cloud`
