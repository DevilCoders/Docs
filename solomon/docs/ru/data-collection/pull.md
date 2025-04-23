# Pull-режим передачи метрик

В pull-режиме передачи метрик Solomon периодически опрашивает пользовательское приложение по протоколу HTTP и ожидает получить ответ в одном из поддерживаемых форматов. Для определения множества опрашиваемых хостов используются различные механизмы [Service discovery](#service-discovery).

Для использования pull-режима пользовательскому приложению необходимо реализовать HTTP endpoint, выполнив запрос к которому Solomon сможет получить значения метрик в одном из поддерживаемых форматов, например, [JSON](./dataformat/json.md).

{% note warning %}

Сбор метрик по протоколу HTTPS не поддерживается.

{% endnote %}

Сбор осуществляется из нескольких реплик, поэтому метрики нельзя очищать или удалять после получения первого запроса за метриками от Solomon.

## Заполнение метки host {#host-label}

В pull-режиме передачи метрик Solomon по умолчанию добавляет к полученным метрикам метку `host`, в значение которой записывается имя хоста (hostname), с которого собраны метрики. Это поведение можно переопределить, явно указывая значение метки `host` вместе со значениями метрик. Чтобы Solomon не добавлял метку `host` к метрика, в качестве ее значения нужно указать пустую строку (`""`).

Чтобы Solomon записывал в метку host не имя хоста, а [FQDN](https://ru.wikipedia.org/wiki/FQDN) (например `solomon-gateway-vla-00.mon.yandex.net` вместо `solomon-gateway-vla-00`), укажите параметр *Use FQDN* в настройках кластера, как показано на Рисунке 1.

![Параметр Use FQDN странице кластера](_assets/use-fqdn.png "Параметр Use FQDN странице кластера"){ width="1552" }
<small>Рисунок 1 — Параметр *Use FQDN* странице кластера.</small>

## Аутентификация {#auth}

В pull-режиме поддерживается опциональная TVM-аутентификация, для того, чтобы пользователькое приложение могло удостовериться, что источник запроса именно Solomon.

Чтобы включить использование TVM-аутентификации, в настройках сервиса в параметре *TVM destination id*  укажите идентификатор TVM-приложения, для которго Solomon получит сервисный TVM-тикет. Идентификаторы TVM-приложений Solomon перечислены в Таблице 1.

![Параметр TVM destination id на странице сервиса](_assets/service-tvm-destination-id.png "Параметр TVM destination id на странице сервиса"){ width="1552" }
<small>Рисунок 1 — Параметр *TVM destination id* на странице сервиса.</small>

<small>Таблица 1 — Идентификаторы и названия TVM-приложений Solomon.</small>

Кластер Solomon | Название приложения | Идентификатор приложения<br/>(TVM client id)
-------|---------|------------
Solomon Production |  solomon-fetcher-prod | 2012028
Solomon Prestable | Solomon fetcher  | 2012024
Solomon Testing | solomon-fetcher-test | 2012026

{% note info %}

TVM-аутентификация в pull-режиме передачи метрик поддерживается только в [кластерах Solomon в Яндексе](../overview/about.md#yandex-clusters).

{% endnote %}

<!--
## Service discovery {#service-discovery}

### Hosts {#hosts}

### Host URLs {#host-url}

### Conductor {#conductor-group}

### Conductor tag {#conductor-tag}

### Nanny {#nanny}

### Qloud {#qloud}

### Network {#netrowk}

### YP clusters {#yp}

### Instance group {#instance-groups}

-->