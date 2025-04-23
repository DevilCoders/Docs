#  Meta 

Это раздел для разработчиков Y.Deploy, позволяющий указывать специальные версии pod_agent, параметры запуска для него и слои для корневой системы пода.

Обычным пользователям не нужно никак указывать этот раздел.

Представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=6549054#L961-984):

##  Бинарник Pod Agent {#pod_agent}

При помощи `url` и `checksum` можно указать конкретную версию pod_agent для загрузки на под.

```yaml
pod_agent_payload:
  meta:
    url: POD_AGENT_BINARY_URL
    checksum: POD_AGENT_BINARY_CHECKSUM
```

##  Слой для запуска Pod Agent {#layer}

При помощи `layers` можно задать особый набор слоев для образа системы, в которой будет запущен `pod_agent`.

```yaml
pod_agent_payload:
  meta:
    layers:
    - url: https://proxy.sandbox.yandex-team.ru/698475424
      checksum: MD5:ea5d47ea8dd4b02a09aaaab82b70199c
```

##  Строка запуска {#command_line}

При помощи `map<string, string> configuration` можно задать дополнительные опции запуска для `pod_agent`.

К строке запуска `pod_agent` будут добавлены элементы вида `-V KEY=VALUE`.



