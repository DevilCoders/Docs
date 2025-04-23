# Документация YP Service Controller (SC)

На этой странице можно узнать:
* Как создаются неспецифичные endpoint'ы
* Что делать, если по какой-то причине они не создались
* Куда идти, если что-то не понятно

## Support Chat

Все вопросы стоит задавать [в чате](https://t.me/joinchat/FUB5vgmFaIpFg-XK).

## Основные понятия

SC использует pod'ы, pod set'ы, endpoint'ы (как результат своей работы) и endpoint set'ы. Подробнее об этих объетках можно узнать в [документации](https://wiki.yandex-team.ru/yp/yp-quick-start-guide/#terminyyp) YP.

В рамках работы SC нас будет особо интересовать небольшое число конкретных полей данных объектов, далее они будут подробнее рассмотрены.

### Endpoint set

* ```[/spec/pod_filter]``` - endpoint'ы будут созданы для pod'ов, соответствующих фильтру
* ```[/spec/liveness_limit_ratio]``` - см. [ниже](#liveness-limit-ratio).

### Pod

* ```[/meta/pod_set_id]``` -  идентификатор pod set'а, которому принадлежит pod
* ```[/status/agent/pod_agent_payload/status/ready/status]``` - статус в pod'а, находящегося под управлением pod agent'а (pod'ы из Деплоя)
* ```[/spec/pod_agent_payload/spec/target_state]``` - target state pod'а, находящегося под управлением pod agent'а
* ```[/status/agent/iss_summary], [/status/iss_conf_summaries]``` - аналогичные состояния статуса и target state'а для pod'a в Nanny YP-Lite в агрегированоом виде. [Тикет](https://st.yandex-team.ru/YP-3307)
* ```[/status/ip6_address_allocations]``` - отсюда берем backbone ipv6 адрес пода

### Endpoint

* ```[/status/ready]``` - статус endpoint'а, определяется логикой, описанной [ниже](#статусы-podов-и-их-связь-со-статусами-endpointов), используя статус и target state pod'а
* ```[/spec/ip6_address]``` - ipv6 адрес pod'а
* ```[/spec/protocol]``` - протокол (tcp/udp), берется из аналогичного /spec поля endpoint set'а
* ```[/spec/port]``` - сетевой порт, берется из аналогичного /spec поля endpoint set'а

## Работа Service Controller'а

SC работает поверх либы контроллеров, то есть циклами синхронизации с YP.

### Supervisor endpoint set'а

Супервизор endpoint set'а - тот, кто отвечает за создание endpoint'ов, например: SC, GenCfg, Samogon. Если данное поле не указано, то по умолчанию супервизором является SC.

На каждом цикле принимаются endpoint set'ы, в которых явно не указано, что SC должен их игнорировать:

`
[/labels/supervisor] != # and [/labels/supervisor] != 'service-controller'
`

В случае, если SC не является супервизором endpoint set'а, в ```[/status/controller/error]``` запишется соответствующая ошибка. К примеру, enpoint'ы GenCfg создаются без участия SC:

```bash
ya tool yp select endpoint_set --filter '[/labels/supervisor] != "service_controller" and [/labels/supervisor] != #' --selector /labels/supervisor --selector /meta/id --selector /status/controller/error --address sas-test --limit 1 --no-tabular
[
    [
        "gencfg";
        "ALICE_GPU";
        {
            "message" = "Sync is ommitted";
            "code" = 0;
            "inner_errors" = [
                {
                    "message" = "Supervisor value is unsuitable";
                    "code" = 0;
                };
            ];
        };
    ];
]
```

Обратите внимание, что данная ошибка не означает, что с endpoint set'ом что-то не так, она лишь говорит о том, что SC не ответственнен за данный объект.

Если у вас нет явной на то причины, рекомендуем не менять настройки супервизора.

### Валидация endpoint set'ов на уровне YP

Как указано в документации YP, у endpoint set'а есть поле [/spec/pod_filter], в котором задаётся фильтр, по которому выбираются pod'ы, до которых нужно создать endpoint'ы. 

Сейчас на стороне YP используется [валидация](https://a.yandex-team.ru/arc_vcs/yp/server/master/objects/endpoint_set_type_handler.cpp?rev=6e2118d4e3be32c8ca6a367e1aa1c336fd402282#L150) этого поля, а именно: 

если фильтр подов задан, то он обязательно должен ограничивать поле ```[/meta/pod_set_id]``` \(Примеры можно изучить в [тестах](https://a.yandex-team.ru/arc_vcs/yp/tests/test_endpoint_sets.py?rev=f17b5e6a03d29a397623dfaecdb91a8e248b359d#L203)\). 

Помимо таких фильтров, допускается использование `[spec/pod_filter]=#`, то есть пустого фильтра, однако, если на то нет особой необходимости, лучше воздержаться, от такой возможности.

Примеры фильтров, ограничивающих поле `[/meta/pod_set_id]`:
```
[/meta/pod_set_id] = "aba"
[/meta/pod_set_id] = "aba" and [/labels/is_that_filter_good] = "yes" and ...
[/meta/pod_set_id] = "aba" and [/meta/pod_set_id] = "xyz"
```
Несмотря на противоречивость последнего фильтра, он всё равно является валидным с точки зрения YP.

Примеры фильтров, которые не пройдут валидацию:
```
1=1
0=1
[/labels/absolutely_bad_filter] = "yes, i think so"
[/meta/pod_set_id] = [/meta/id]
[/meta/pod_set_id] = [/meta/pod_set_id]
not ([/meta/pod_set_id] != "aba")
[/meta/pod_set_id] IN ("1", "2", "3")
[/meta/pod_set_id] = "1" OR [/meta/pod_set_id] = "2" OR [/meta/pod_set_id] = "3"
```
TODO: в будущем появится возможность использовать фильтры того же типа, что последний. См. [тикет](https://st.yandex-team.ru/YP-3747).

Убедительная просьба: если вам кажется, что фильтр, который вы планируете использовать, выглядит странно или вы не видели подобных фильтров в примерах и тестах, уточните у нас в [чате](https://t.me/joinchat/FUB5vgmFaIpFg-XK) и затем создайте такой endpoint set на кластере YP SAS-TEST ради избежания возможных проблем.

Исключением являются endpoint set'ы, созданные super user'ами YP или созданные до существования этой валидации. Подробнее о мотивации такой валидации можно почитать в [YP-3272](https://st.yandex-team.ru/YP-3272).

### Валидация endpoint set'ов на уровне SC

#### Пустые фильтры

Несмотря на то, что YP разрешает пустые `[endpoint_set/spec/pod_filter]=#`, SC не обработает такие объекты, а в поле `[/status/controller/error]` запишет соответствующую ошибку:

```bash
ya tool yp select endpoint_set --filter '([/labels/supervisor] = "service_controller" or [/labels/supervisor] = #) and [/spec/pod_filter]=#' --selector /labels/supervisor --selector /meta/id --selector /status/controller/error --address sas-test --limit 1
[
    [
        #;
        "9d2ec32lstkil76g";
        {
            "message" = "Sync is ommitted";
            "code" = 0;
            "inner_errors" = [
                {
                    "message" = "Pod filter is empty";
                    "code" = 0;
                };
            ];
        };
    ];
]
```

#### Вайтлист SC

SC валидирует поля, которые можно использовать в фильтре, при помощи [вайтлиста](https://a.yandex-team.ru/arc_vcs/infra/service_controller/libs/daemon/config.json?rev=47c569075575a82750d356d2dc86511ba54572af#L43). 

Примеры фильтров, который не проходит валидацию по вайтлисту, но проходит валидацию YP:
```
[/meta/pod_set_id] = "some_pod_set_id" AND [/labels/banned_label] = "123"
[/meta/pod_set_id] = "some_pod_set_id" AND [/labels/banned_label] = #
[/meta/pod_set_id] = "other_pod_set_id" AND [/status/agent/iss_summary] != #
```

В этом случае пользователь может увидеть ошибку в поле endpoint set'а `[/status/controller/error]`:
```bash
"controller" = {
    "error" = {
        "message" = "Sync is ommitted";
        "code" = 0;
        "inner_errors" = [
            {
                "message" = "Selector [...] in pod_filter is not in whitelist";
                "code" = 0;
            };
        ];
    };
};

```

###

Если вам нужно новое поле для фильтрации подов, или у вас есть строгая необходимость в пустом фильтре, и вы уверены, что иначе вам не обойтись, напишите нам в [чате](https://t.me/joinchat/FUB5vgmFaIpFg-XK).

### Статусы pod'ов и их связь со статусами endpoint'ов

Для того, чтобы определить статус endpoint'a, SC определяет текущий статус и target state соответствующего pod'a. Pod'ы делятся на 2 типа:
* С Pod Agent'ом для Deploy'a: `state == ready if pod.status == ready && pod.target_state != removed && pod.target_state != suspended`
* Без Pod Agent'а для Nanny: `state == ready if pod.current_state == active || exists pod.instance: pod.instance.target_state == active`

Для них различается логика определения статуса ready. Подробнее в соответствующем [коде](https://a.yandex-team.ru/arc_vcs/infra/service_controller/libs/endpoint_set_controller/endpoint_set_controller.cpp?rev=db4adf1391908615e392e1a5176e22951734d443#L103-114).

### Liveness limit ratio

Для каждого endpoint set'а можно задать поле `[spec/liveness_limit_ratio]` - число в пределах `[0;1]`, отвечающее за то, сколько неактивных endpoint'ов стоит не удалять для данного endpoint set'а.

```ceil(liveness_limit_ratio * pods_count) <= endpoints_count```

Другими словами: если в каком-то случае все поды, относящиеся к одному endpoint'у, потеряли статус active с точки зрения SC, то соответствующие им неактивные endpoint'ы не будут удалены.

По умолчанию принимает значение `0.0`, то есть SC может удалить все endpoint'ы. Если вы не уверены, стоит ли ограничивать это значение, рекомендуем выставить значение `1.0`. Подробнее в [тикете](https://st.yandex-team.ru/YP-1502).


## Время цикла синхронизации

На данный момент SC работает порядка 30 секунд на SAS (самый большой кластер с точки зрения резолва endpoint set -> pods). 

График можно найти в [Мониторинге](https://nda.ya.ru/t/l9U50Hi74mCibu).

[Тикет](https://st.yandex-team.ru/DISCOVERY-167) на починку горизонтальной линии на графике.

## Как пользователю получить получить список endpoint'ов 

Для того, чтобы получить endpoint'ы по данному endpoint set'у, можно воспольоваться соответствующей [ручкой YP Service Discovery](https://docs.yandex-team.ru/yp-service-discovery/#ruchki).
