# SSS: сервис скликивания

Запуск:

```bash
ya make && ./sss
```

На `http://127.0.0.1:8080` поднимется веб-сервер.

По корню [http://127.0.0.1:8080](http://127.0.0.1:8080) доступна Swagger-спецификация.

Поддерживается POST-запрос на ручки

### `/parse`:

 ```bash
curl -X POST -H "Content-type: application/json" [::1]:8080/parse -d @tests/data/payload.json
```

формат данных:

```json
{
  "content": "{...}",
  "parser": "YandexBaobabParser"
}
```

Ключ `"parser"` можно опустить, тогда будет использован `YandexBaobabHTMLParser`.

### `/parsers` (она же `/engines`)

```bash
curl [::1]:8080/parsers
```

возвращает список доступных парсеров.

### `/prepare`

```bash
curl -X POST -H "Content-type: application/json" [::1]:8080/prepare -d @tests/data/queries_configs.json
```

по модальному запросу и конфигу отдает soy-curl

`/prepare-and-download`, `/prepare-and-download-and-parse`, `/prepare-and-download-and-parse-and-convert` являются аналогами ручек `/download`, `/download-and-parse`, `/download-and-parse-and-convert`, которые принимаю модальный запрос и конфиг вместо soy-curl

## Переменные окружения

* `SSS_HOST` (по умолчанию `::`)
* `SSS_PORT` (по умолчанию `8080`)

## Docker

Сервис собирается в Docker-образ. Образы хрянятся в репозитории `qe_quality/metrics_sss`. Права на репозиторий выдаются [через IDM](https://idm.yandex-team.ru/group/42800/roles?page=2#f-status=all,sort-by=system,role=16662849).

### Авторизация в Registry

* Нужно получить токен https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
* Логинимся в registry:

    ```bash
    sudo docker login -u <login> --password-stdin registry.yandex.net
    <token_body><Enter>
    ^D(иногда может понадобиться еще один ^D, третий раз только не надо - выйдете из консоли)
    ```

Посмотреть список тэгов:

```bash
curl -H "Authorization: OAuth ${REGISTRY_TOKEN}" https://registry.yandex.net/v2/qe_quality/metrics_sss/tags/list | jq '.tags | sort'
```

## CI/CD

CI-Job'а `Deploy docker metrics sss` ([timeline](https://a.yandex-team.ru/projects/metric/ci/actions/launches?dir=ci%2Fregistry%2Fprojects%2Ftestenv%2Fmetrics&id=deploy-docker-metrics-sss)) создает Docker-образы и размещает их в Registry. Наблюдаются три директории:

- `search/metrics/sss`
- `search/metrics/monitoring`
- `search/scraper/parser_platform`

Создается образ вида `qe_quality/metrics_sss:6915935`, тэг берется из ревизии (`Merged as r6915935`).

## Ручное обновление Docker-образа

[Документация Registry](https://wiki.yandex-team.ru/qloud/docker-registry/)

### Сборка

```bash
docker build . -t qe_quality/metrics_sss:manual_<номер>
```

При сборке на Ubuntu в папке `arc` замечена ошибка `unable to prepare context: path "." not found`.
Можно скопировать `sss` и `Dockerfile` в другую папку, изменить в нём путь.

### Запуск

```bash
docker run -p 1729:8080 --name sss --rm qe_quality/metrics_sss:manual_<номер>
```

### Обновление в Registry

```bash
docker tag qe_quality/metrics_sss:manual_<номер> registry.yandex.net/qe_quality/metrics_sss:manual_<номер>
docker push registry.yandex.net/qe_quality/metrics_sss:manual_<номер>
```

### Обновление образа в Deploy

В Deploy находим [конфигурацию](https://deploy.yandex-team.ru/project/quality_metrics-sss_dev/config), нажимаем edit и обновляем тэг образа.

![скриншот](https://jing.yandex-team.ru/files/leshapak/2020-04-28%2015-05-34%20Yandex%20Deploy-2.png)
