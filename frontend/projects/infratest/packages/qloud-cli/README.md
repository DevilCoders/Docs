# qloud-cli

Консольный клиент для qloud

## Полезная информация

* Базируется на [qloud-api](https://github.yandex-team.ru/qloud/qloud-api)
* [Документация публичного API qloud](https://docs.qloud.yandex-team.ru/doc/api/)

## Установка

```sh
npm install -g @yandex-int/si.ci.qloud-cli

export QLOUD_OAUTH_TOKEN={TOKEN}
```

`qloud-cli` будет использовать токен из переменной окружения `QLOUD_OAUTH_TOKEN`.

Если такая переменная окружения не указана, то из `QLOUD_API_OAUTH_TOKEN` или `QLOUD_API_TOKEN`.

Рекомендуется использовать `QLOUD_OAUTH_TOKEN`. Остальные варианты были добавлены по историческим причинам.

## Доступные команды

### qloud-cli

```console
  Usage: qloud-cli [options] [command]


  Commands:

    component     Управление компонентами
    environment   Управление окружениями
    domain        Управление доменами
    route         Управление роутингом
    help [cmd]    display help for [cmd]

  Options:

    -h, --help     output usage information
    -V, --version  output the version number

```

### qloud-cli  component

```console
  Usage: qloud-cli-component [options] [command]


  Commands:

    add <environmentId> <componentType> <componentName>  Создание компонента или сервиса
    get <componentId> [version]                          Загрузить детали компонента
    deploy [options] <componentId> [version]             Развернуть новую версию
    delete <componentId>                                 Удалить компонент/сервис

  Options:

    -h, --help  output usage information

```

### qloud-cli  component  add

```console
  Usage: add [options] <environmentId> <componentType> <componentName>

  Создание компонента или сервиса

  Options:

    -h, --help  output usage information

```

### qloud-cli  component  get

```console
  Usage: get [options] <componentId> [version]

  Загрузить детали компонента

  Options:

    -h, --help  output usage information

```

### qloud-cli  component  deploy

```console
  Usage: deploy [options] <componentId> [version]

  Развернуть новую версию

  Options:

    -h, --help                                                               output usage information
    -t, --type [type]                                                        Тип компонента
    --max-fails [maxFails]                                                   Максимальное количество ошибок, после которого роутер будет считать компонент мертвым
    --default-max-fails [defaultMaxFails]                                    Значение по умолчанию, рекомендуемое для --max-fails
    --fail-timeout [failTimeout]                                             Промежуток времени (ms), в течение которого роутер не будет пытаться проверить, не ожил ли компонент
    --default-timeout [defaultFailTimeout]                                   Значение по умолчанию, рекомендуемое для --fail-timeout
    --proxy-connect-timeout [proxyConnectTimeout]                            nginx.org#proxy_connect_timeout
    --default-proxy-connect-timeout [defaultProxyConnectTimeout]             значение по умолчанию, рекомендуемое для --proxy-connect-timeout
    --proxy-read-timeout [proxyReadTimeout]                                  nginx.org#proxy_read_timeout
    --default-proxy-read-timeout [proxyReadTimeout]                          значение по умолчанию, рекомендуемое для --proxy-read-timeout
    --proxy-write-timeout [proxyWriteTimeout]                                nginx.org#proxy_send_timeout
    --default-proxy-write-timeout [proxyWriteTimeout]                        значение по умолчанию, рекомендуемое для --proxy-write-timeout
    --proxy-next-upstream [proxyNextUpstream]                                nginx.org#proxy_next_upstream
    --default-proxy-next-upstream [defaultProxyNextUpstream]                 значение по умолчанию, рекомендуемое для --proxy-next-upstream
    --proxy-next-upstream-timeout [proxyNextUpstreamTimeout]                 nginx.org#proxy_next_upstream_timeout
    --default-proxy-next-upstream-timeout [defaultProxyNextUpstreamTimeout]  значение по умолчанию, рекомендуемое для --proxy-next-upstream-timeout
    --proxy-next-upstream-tries [proxyNextUpstreamTries]                     nginx.org#proxy_next_upstream_tries
    --default-proxy-next-upstream-tries [defaultProxyNextUpstreamTimeout]    значение по умолчанию, рекомендуемое для --proxy-next-upstream-tries
    --use-https [useHttps]                                                   Если установлено в true, то обращение к соответствующему компоненту или внешним серверам (в случае балансера) будет по https
    --use-client-certificate [useClientCertificate]                          Если установлено в true, то обращение к соответствующему компоненту или внешним серверам (в случае балансера) будет с авторизацией с клиентским сертификатом. Если true, то useHttps тоже устанавливается в true при сохранении
    --client-certificate [clientCertificate]                                 сертификат в pem-формате, как в domain management
    --units [units]                                                          общее количество инстансов сумма по (instanceGroups)
    --allocated-units [allocatedUnits]                                       фактическое количество инстансов (может быть меньше units если не хватило ресурсов для деплоймента)
    --network [network]                                                      сеть, в настоящее время может быть QLOUDNETS или SEARCHSAND
    --size [network]                                                         размер инстанса ("t1_small" .. "c1_enterprise")
    --component-environment [componentEnvironment]                           UNIX-environment данного компонента в виде текста (дополнительно будут добавлены переменные, определенные на уровне окружения)
    --stdout [stdout]                                                        указание на содержание стандартного потока вывода. Допустимые значения: ignored - не передавать содержимое в elasticsearch, line - считать каждую строку отдельным сообщением, json - ожидать в потоке сообщения в json формате.
    --stderr [stderr]                                                        указание на содержание стандартного потоков вывода. Допустимые значения: ignored - не передавать содержимое в elasticsearch, line - считать каждую строку отдельным сообщением, json - ожидать в потоке сообщения в json формате.
    --generate-qloud-peers [generateQloudPeers]                              Qloud будет добавлять в окружение переменную QLOUD_PEERS, содержащую через запятые список всех инстансов компонента (полностью квалифицированные имена хостов контейнеров)
    --repository [repository]                                                Docker URL по которому можно скачать image, например, repository.qloud.yandex.net/myProject/mayApp:1.2
    --hash [hash]                                                            хеш образа, который нужно запускать

```

### qloud-cli  component  delete

```console
  Usage: delete [options] <componentId>

  Удалить компонент/сервис

  Options:

    -h, --help  output usage information

```

### qloud-cli  environment

```console
  Usage: qloud-cli-environment [options] [command]


  Commands:

    new <environmentName> <applicationId>        Создание нового пустого окружения
    fork [options] <environmentName> <originId>  Создание копии существующего (развернутого) окружения в виде нового черновика
    get [options] <environmentId> [version]      Получить версию окружения
    delete [options] <environmentId>             Удалить окружение
    dump <environmentId>                         Получить дамп окружения
    deploy [options] <environmentId>             Развернуть новую версию
    env <environmentId> <userEnvironment>        Создание или изменение пользовательских переменных среды
    upload [options]                             Позволяет в одну операцию загрузить окружение и сразу задеплоить. По-умолчанию использует stdin

  Options:

    -h, --help  output usage information

```

### qloud-cli  environment  new

```console
  Usage: new [options] <environmentName> <applicationId>

  Создание нового пустого окружения

  Options:

    -h, --help  output usage information

```

### qloud-cli  environment  fork

```console
  Usage: fork [options] <environmentName> <originId>

  Создание копии существующего (развернутого) окружения в виде нового черновика

  Options:

    -h, --help                            output usage information
    -C, --copy-variables [copyVariables]  Копировать переменные окружения

```

### qloud-cli  environment  get

```console
  Usage: get [options] <environmentId> [version]

  Получить версию окружения

  Options:

    -h, --help           output usage information
    -d, --draft [draft]  Показать черновик

```

### qloud-cli  environment  delete

```console
  Usage: delete [options] <environmentId>

  Удалить окружение

  Options:

    -h, --help           output usage information
    -d, --draft [draft]  Удалить черновик

```

### qloud-cli  environment  dump

```console
  Usage: dump [options] <environmentId>

  Получить дамп окружения

  Options:

    -h, --help  output usage information

```

### qloud-cli  environment  deploy

```console
  Usage: deploy [options] <environmentId>

  Развернуть новую версию

  Options:

    -h, --help                       output usage information
    -k, --keepSandbox [keepSandbox]  Не удалять черновик

```

### qloud-cli  environment  env

```console
  Usage: env [options] <environmentId> <userEnvironment>

  Создание или изменение пользовательских переменных среды

  Options:

    -h, --help  output usage information

```

### qloud-cli  environment  upload

```console
  Usage: upload [options]

  Позволяет в одну операцию загрузить окружение и сразу задеплоить. По-умолчанию использует stdin

  Options:

    -h, --help               output usage information
    -f, --file [file]        Загрузить из файла
    -r, --require [require]  Подключить файл как npm модуль

```

### qloud-cli  domain

```console
  Usage: qloud-cli-domain [options] [command]


  Commands:

    list <environmentId>                         Получить домены окружения
    edit [options] <environmentId> <domainName>  Добавить домен
    delete <environmentId> <domainName>          Удалить домен

  Options:

    -h, --help  output usage information

```

### qloud-cli  domain  list

```console
  Usage: list [options] <environmentId>

  Получить домены окружения

  Options:

    -h, --help  output usage information

```

### qloud-cli  domain  edit

```console
  Usage: edit [options] <environmentId> <domainName>

  Добавить домен

  Options:

    -h, --help                       output usage information
    -c, --certificate [certificate]  Сертификат в pem-формате
    --httpAllowed [httpAllowed]      Разрешить доступ по http
    --httpOnly [httpOnly]            Разрешить доступ только по http
    --l7path [l7path]                Только для L7 и cdn доменов
    -t, --type [type]                Тип домена
    --moveTo [moveTo]                Переместить в другое окружение

```

### qloud-cli  domain  delete

```console
  Usage: delete [options] <environmentId> <domainName>

  Удалить домен

  Options:

    -h, --help  output usage information

```

### qloud-cli  route

```console
  Usage: qloud-cli-route [options] [command]


  Commands:

    add [options] <environmentId> <location> <componentName>  Изменение сразу всей таблицы маршрутизации маршрута

  Options:

    -h, --help  output usage information

```

### qloud-cli  route  add

```console
  Usage: add [options] <environmentId> <location> <componentName>

  Изменение сразу всей таблицы маршрутизации маршрута

  Options:

    -h, --help                                             output usage information
    --proxyPolicy [proxyPolicy]
    --upstreamPath [upstreamPath]
    --geo [geo]
    --preAuthenticate [preAuthenticate]
    --yandexErrorPage [yandexErrorPage]
    --proxyConnectTimeout [proxyConnectTimeout]
    --proxyReadTimeout [proxyReadTimeout]
    --proxyWriteTimeout [proxyWriteTimeout]
    --proxyNextUpstream [proxyNextUpstream]
    --proxyNextUpstreamTimeout [proxyNextUpstreamTimeout]
    --proxyNextUpstreamTries [proxyNextUpstreamTries]

```
