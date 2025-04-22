# Управление скоростью деплоя

В Деплое существует возможность управлять скоростью выкатки новой ревизии сервиса без изменения спеки сервиса.
Возможные сценарии, когда это может пригодиться:
* выкатывается новый релиз, по метрикам видно, что что-то идет не так и хочется остановить выкатку изменений на 100% подов, не откатываясь на предыдущую ревизию. Для этого достаточно выставить disruption budget = 0. Важно отметить, что при этом также останавливается [эвакуация](../reference/internals/architecture/rsc.md#eviction) подов.
* откат (по факту применение старой ревизии спеки сервиса) - в экстренных случаях хочется производить как можно быстрее с повышенным [Disruption budget](../concepts/deploy-unit/deploy-primitives.md#disruption-budget). 

{% note info %}

1. Переопределение deployment strategy работает только в рамках текущей ревизии спеки и будет сброшено при следующем изменении настроек сервиса.
2. Перегрузка опций deployment strategy не приводит к изменению ревизии deploy unit'а.

{% endnote %}

## Механика
Механика изменения настроек deployment strategy (на данный момент доступно только переопределение параметра max_unavailable, соответствующего disruption budget) работает для определенной ревизии деплой юнита и перечня кластеров, к которому применяются изменения.

Настроить временное изменение значений deployment strategy возможно ручным вызовом команды в **dctl** или **YP API**, либо в **UI**.

### UI
В UI для каждого replica set'a deploy unit'a есть таб `Disruption budget`, где можно переопределить значение. Все параметры (текущая ревизия и значение disruption budget) будут взяты из текущего деплой юнита и показаны в сообщении при подтверждении действия.
![override-db](../_assets/how-to/override-db.png)

### dctl
В `dctl` переопределение deployment strategy выполняется при помощи следующей команды:
```bash
ya tool dctl control stage override_deployment_strategy <stage_id> --cluster-to-override sas --cluster-to-override man --revision <revision> --deploy-unit-id <deploy_unit_id> --max-unavailable 3 -c xdc
```

В данном примере:
* `control stage override_deployment_strategy` - указывает операцию переопределения deployment strategy для стейджа <stage_id>
* `--deploy-unit-id` - имя deploy unit'а, для которого переопределяется deployment strategy
* `--revision` - ревизия deploy unit'а, для которой переопределяется deployment strategy
* `--cluster-to-override` - кластер, к которому должны примениться изменения (может быть несколько значений)
* `--max-unavailable` - новое значение disruption budget'а
* `-c xdc` - кластер YP, в котором вносятся изменения (для настроек стейджей всегда XDC)

Указанная ревизия должна обязательно соответствовать текущей ревизии деплой юнита, деплой юнит должен существовать, кластера должны быть использованы в деплой юните, иначе будет ошибка валидации.

### YP API
Пример переопределения deployment strategy через YP API:

```bash
ya tool yp update stage <stage_id> --set /control/override_deployment_strategy '{max_unavailable={deploy_unit_id=deployUnit;revision=16;value=3;clusters=[sas;man;];};}' --address xdc
```

В данном примере:
* `yp update stage` - указывает операцию обновления настроек стейджа <stage_id>
* `--set /control/override_deployment_strategy` - указывает на поле в стейдже (контрол override_deployment_strategy), в которое записываются изменения в json-формате 
* `--address xdc` - кластер YP, в котором вносятся изменения (для настроек стейджей всегда XDC)

Параметры json payload'а:
* `max_unavailable` - объект с настройками переопределения disruption budget'а
    * `deploy_unit_id` - имя deploy unit'а, для которого переопределяется deployment strategy
    * `revision` - ревизия deploy unit'а, для которой переопределяется deployment strategy
    * `clusters` - список кластеров, к которому должны примениться изменения
    * `value` - новое значение disruption budget'а

Указанная ревизия должна обязательно соответствовать текущей ревизии деплой юнита, деплой юнит должен существовать, кластера должны быть использованы в деплой юните, иначе будет ошибка валидации.


## FAQ
Q: Я хочу, чтобы настройки перегрузки применились до начала выкладки, как это сделать?
A: **Пользуйтесь транзакциями YP или [полокационной выкладкой с подтверждением](../concepts/perlocation.md).**

Q: Будет ли видно, кто изменил настройки выкладки в какой-то момент времени?
A: **Да, запоминается логин владельца токена и потом это планируется отображать в истории.**


