# http_proxy_cache

Микросервис, проксирует http-запросы, кеширует ответы
* Расположение в Platform (QLoud): https://platform.yandex-team.ru/projects/rasp/http-proxy-cache
* Релизная машина https://rm.z.yandex-team.ru/component/rasp_http_proxy_cache

## Go в Аркадии

https://wiki.yandex-team.ru/devrules/go/
главное прописать правильные $GOPATH и $GOROOT
https://wiki.yandex-team.ru/devrules/Go/getting-started/#arc

## Запуск бинарника
Для локальной работы достаточно сбилдить бинарник и запустить
```
cd $GOPATH/src/a.yandex-team.ru/travel/rasp/http_proxy_cache/cmd/hpc
ya make
RASP_VAULT_OAUTH_TOKEN=<token> YENV_TYPE=development CONFIG_PATH=$GOPATH/src/a.yandex-team.ru/travel/rasp/http_proxy_cache/config.development.yaml ./hpc
```

### Запуск в GoLang от JetBarins
примерно так должна выглядеть конфигурация для запуска:
```
Run kind: package
Package Path: a.yandex-team.ru/travel/rasp/http_proxy_cache/cmd/hpc
Working Directory: /Users/ganintsev/go/src/a.yandex-team.ru/travel/rasp/http_proxy_cache/cmd/hpc
Environment: RASP_VAULT_OAUTH_TOKEN=<token>;YENV_TYPE=development;CONFIG_PATH=/Users/ganintsev/go/src/a.yandex-team.ru/travel/rasp/http_proxy_cache/config.development.yaml
```

## YAML-конфиг

локально можно скопировать себе config.development.yaml, исправить все что нужно и указывать свой путь при запуске
```
redis: # блок настроек бд Redis для кеширования
  addrs:
    - host1.yandex.net:26379
    - host2.yandex.net:26379
  master_name: raas_testing_http_proxy_cache
log: # блок настроек логирования
  is_production_config: true # если true, то лог в json формате
  level: INFO
server: # основные настройки приложения
  port: 8085 # прослушиваемый порт
  services: # список проксируемых сервисов
    -
      base_path: /morda_backend # путь для роутинга
      backend: https://testing.morda-backend.rasp.yandex.net # адрес проксируемого сервиса
      backend_timeout: 15s # таймаут до проксируемого сервиса
      caching: # блок настроек кеширования
        ignore_query_params: # список игнорируемых при кешировании параметров запроса
          - _rid
        time_to_live: 24h # время жизни записи в redis
        time_to_refresh: 1h # время, через которое, запись считается устаревшей и обновляется в фоне
```

на практике такой конфиг значит, что для получения кешированных результатов на запросы

https://testing.morda-backend.rasp.yandex.net/ru/segments/min-tariffs/?pointFrom=c2&pointTo=c213&transportType=train&national_version=ru&_rid=e4a9f787-56f8-4a3c-9122-a2a5d920703b

можно ходить по адресу

http://localhost:8085/morda_backend/ru/segments/min-tariffs/?pointFrom=c2&pointTo=c213&transportType=train&national_version=ru&_rid=e4a9f787-56f8-4a3c-9100-a2a5d920703b

при этом:
* будет сформирован ключ /morda_backend/ru/search/search/?nationalVersion=ru&pointFrom=c2&pointTo=c213&transportType=train
* при первом таком запросе в кеше пусто и пойдем в backend, закешируем ответ
* при повторном запросе через время < time_to_refresh вернем ответ из кеша
* при повторном запросе через время > time_to_refresh вернем ответ из кеша, в фоне обновим кеш из backend, время кеша также обновляется
* если втечение time_to_live таких запросов не было, то в кеше пусто
