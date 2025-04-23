# Настройка поставки метрик в yasm

## Введение {#intro}

Речь пойдёт про метрики приложения. А точнее, как поставлять свои метрики в yasm по pull-схеме через стат-ручку. Оригинальная документация yasm [тут](https://wiki.yandex-team.ru/golovan/userdocs/stat-handle/?from=%252Fgolovan%252Fstat-handle%252F).

## Подготовка приложения {#prepare}

Приложение отвечает метриками в json формате на порту 8080 и `path=/unisat`

![https://jing.yandex-team.ru/files/x0leg/Screenshot%20from%202019-08-08%2020-30-28.png](https://jing.yandex-team.ru/files/x0leg/Screenshot%20from%202019-08-08%2020-30-28.png)

## Конфигурируем стат-ручку {#unistat}

Необходимо в поле `unistat` и `port` задать соответствующие значения. В данном примере `unistat=/unistat` `port=8080`

В proto-спеке настройки мониторингов находятся в поле `TPodSpec.host_infra.monitoring` (внутри `pod_template_spec.spec` в деплой-юните). [Схема](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/host_infra.proto).

Unistat-ручки прописываются в `TMonitoringInfo.unistats`.

Можно настраивать собственные теги. Общие теги на pod указываются в `TMonitoringInfo.labels` - они будут приписаны ко всем объектам, относящимся к pod (box, volume, unistat, etc). Для отдельных unistat-ручек можно определить дополнительные теги или переопределить общеподовые в `TMonitoringUnistatEndpoint.labels`.

### Схема тегов {#tags-scheme}

Из [стандартных тегов](https://wiki.yandex-team.ru/golovan/userdocs/faq/#jadolzheninterpretirovatjetitegikak-toosobenno) остается `itype`. Сейчас пользователь может задать его произвольно, но планируется, что со временем туда будет выставляться имя проекта (потому что к нему привязаны квоты на сигналы). Сейчас, если пользователь не указал `itype`, то будет выставлен `itype=deploy`.

К каждому объекту приписываются Деплой-специфичные теги:
* `stage` — stage, к которому он относится.
* `deploy_unit` — deploy_unit, к которому он относится.
* `box` — для porto-метрик box — имя box, с которого они сняты.
* `volume` — для porto-метрик volume — имя volume, с которого они сняты.

Помимо этого, пользователь может задавать собственные теги, привязанные к его `itype`, [согласно инструкции](https://wiki.yandex-team.ru/golovan/userdocs/user-tags/), а также старые yasm-теги (prj, ctype, tier и другие).

## Проверка наличия метрик в yasm {#yasm}

![https://jing.yandex-team.ru/files/x0leg/Screenshot%20from%202019-08-08%2018-26-22.png](https://jing.yandex-team.ru/files/x0leg/Screenshot%20from%202019-08-08%2018-26-22.png)
