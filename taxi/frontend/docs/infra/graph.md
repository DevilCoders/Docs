# Графики сервиса

Графики сервиса (нагрузка в rps и статусы ответов) доступны в [графане](https://grafana.yandex-team.ru) и по дефолту содержат лишь график балансера, что не очень информативно.
Обычно хочется, как минимум, разделить нагрузку на nodejs часть или видеть нагрузку на конкретные urls вашего сервиса. Настроить графики можно через pr в репозиторий [taxi/infra/infra-cfg-graphs](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/infra/infra-cfg-graphs/dorblu/taxi).
1. Ищем файл вашего сервиса, примерное имя **nanny.taxi_{service}_stable.yaml**
2. Добавляем необходимые вам правила, можно на примере соседних файлов, либо ознакомиться [с документом](https://wiki.yandex-team.ru/taxi-infra/dorblu/?from=%2Fjandekskarty%2Fadmining%2Ftech%2Fdorblu%2F)
3. Обязательно убедитесь, что у вас есть правило на ping + оно должно иметь имя `{rtc-service-name}.yandex.net/ping_GET:`, т.к. фигурирует в расчете [uptime](https://wiki.yandex-team.ru/taxi/backend/hejmdal/aptajjm-rtc-servisa/#uchetrpsruchkipingprivychisleniiaptajjma) сервиса [Пример](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/infra/infra-cfg-graphs/dorblu/taxi/nanny.taxi_card-filter_stable.yaml?rev=r9356274#L17).

{% cut "screen" %}

![](https://jing.yandex-team.ru/files/twin/grafana.png)

{% endcut %}

Чат [taxi-diagnostics-support](https://t.me/+Dvagm3dTAkYwMzQ6)

Там же, здесь можно найти ссылки на графики в **yasm**, с данными о потребляемых ресурсах. 

Графики **балансера** и **антиробота** на нём можно найти в nanny:
1. Открываем вкладку [awacs](https://nanny.yandex-team.ru/ui/#/awacs) в nanny
2. Ищем ваш сервис
3. Проваливаемся во вкладку monitoring

{% cut "screen" %}

![](https://jing.yandex-team.ru/files/twin/awacs1.png)
![](https://jing.yandex-team.ru/files/twin/awacs2.png)

{% endcut %}

[Запись](https://wiki.yandex-team.ru/taxi/frontend/grafiki-i-alerty/) рассказа от группы эксплуатации про графики