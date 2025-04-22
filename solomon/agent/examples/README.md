Каталог примеров использования Агента с соответствующими файлами [конфигураций](https://wiki.yandex-team.ru/solomon/agent/how-to-run/#konfigagenta)

## TL;DR
Запустить агент с proto&#42; конфигом `example.conf`:
```bash
$ ../bin/solomon-agent --config example.conf
```

&#42; Также поддерживается json

Проверить, какие данные сейчас находятся в хранилище Агента для проекта `my_project` и сервиса `my_service`:
- http://localhost:8080/storage/find?project=my_project&service=my_service&pretty=true (только метки сенсоров)
- http://localhost:8080/storage/read?project=my_project&service=my_service&limit=2&pretty=true (метки и значения)

Для более подробного понимания работы, см. ниже

## Важное для понимания
### **Push** и **Pull** модели доставки данных:
<details>

Агент -- связующее звено между Соломоном и источниками данных, а значит всего есть две связи:
Соломон <--> Агент и Агент <--> источники данных.

#### Соломон <--> Агент
<a href="https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/solomon/agent/examples/Solomon_Agent.png?repo=arc">
    <img src="https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/solomon/agent/examples/Solomon_Agent.png?repo=arc" width="600px">
</a>

Данные в Соломон попадают двумя путями:
- **Pull** модель доставки данных. Solomon Fetcher периодически опрашивает Агент и забирает накопленные сенсоры. Для этого Соломону нужно знать информацию об Агенте, которого он будет опрашивать (указывается в настройках сервиса Соломона).
- **Push** модель доставки данных. Агент периодически отправляет накопившиеся данные в Соломон через [Push API](https://wiki.yandex-team.ru/solomon/api/push/). Соломон при этом про Агента ничего не знает -- именно в конфиге Агента указыается, по какому адресу следует отправлять данные в Соломон.

#### Агент <--> источники данных
<a href="https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/solomon/agent/examples/Agent_sources.png?repo=arc">
    <img src="https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/solomon/agent/examples/Agent_sources.png?repo=arc" width="600px">
</a>

При этом Агент также может получать данные разными способами:
- **Pull**. Агент сам опрашивает источники. Ими могут быть Python модули, операционная система (CPU, Storage, etc.), http сервисы и т.д.
- **Push**. Данные в Агент приходят напрямую от источника. Например, источник отправляет HTTP запрос формате [Push API](https://wiki.yandex-team.ru/solomon/api/push/).

Таким образом, полная картина выглядит как:

<a href="https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/solomon/agent/examples/full_relation.png?repo=arc">
    <img src="https://a.yandex-team.ru/api/tree/blob/trunk/arcadia/solomon/agent/examples/full_relation.png?repo=arc" width="800px">
</a>


</details>

Если не указано явно, под **push** и **pull** будет подразумеваться то, как Соломон получает данные от Агента. Т.е. "Агент в push режиме" означает, что
Агент отправляет данные в Соломон через [Push API](https://wiki.yandex-team.ru/solomon/api/push/). Как при этом Агент получает данные от источников, в данном контексте не важно.

### Особенности работы в Push режиме:
При сохранении данных в локальное хранилище Агент разбивает данные на шарды, оперируя только значениями **project** и **service**. Значение **cluster** в Pull режиме выставляется на стороне Соломона, т.к. ему известно, какие кластеры он будет опрашивать. Таким же образом выставляется метка **host**. Но т.к. в push режиме Агент сам должен владеть всей информацией, необходимо выставлять значение **Cluster** в пуш конфиге явно. Для указания **host** можно добавить в конфиг Агента новый common label -- `Labels: ["host=host_value"]` -- или выставить переменную окружения `SA_HOST`.

## Примеры
- [Минимальная **push** конфигурация](push/minimal-push)
- [Минимальная **pull** конфигурация](pull/minimal-pull)
- [**Push** с авторизацией](push/push-auth)
- [**Push** с разбиением данных на несколько шардов](push/push-cross-shard)
- [**Push** до Соломона, **Pull** до модулей](push/solomon-push-modules-pull)
- [**Push** до Соломона, **Push** до модулей](push/solomon-push-modules-push)
- [**Pull** до Соломона, **Pull** до модулей](pull/solomon-pull-modules-pull)
- [**Pull** до Соломона, **Push** до модулей](pull/solomon-pull-modules-push)

#### Advanced
- [Использование доп. тредпулов, указание логирования и размера хранилища](advanced/thread-pools-log-storage)
- [Работа в обоих режимах (Push, Pull) сразу с созданием новых шардов](advanced/push-pull-simultaneously)
- [Предагрегация на стороне Агента](advanced/aggregating-storage)
