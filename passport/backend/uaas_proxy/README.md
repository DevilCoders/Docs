## passport-uaas-proxy

Демон ручки, проксирующей эксперименты из uaas.
+демон ручки, отдающей дивные карточки для АМ + мессенджера

### Ключевые моменты
* На `go`
* Используется `easyjson` вместо `json`, потому что это значительно быстрее по профайлеру
* правила переписывания экспериментов прямо в коде в `internal/experiments_rewriter.go`
* mobileproxy nginx проксирует запросы в deploy

### Как запустить
```
cd passport/backend/uaas_proxy
ya make -tt
./cmd/passport-uaas-proxy -c config/config.development.json

curl -vv localhost/uaas
curl localhost:8081/unistat | python -mjson.tool
```

### Полезные ссылки
#### Deploy
Прод: https://deploy.yandex-team.ru/stage/passport-uaas-proxy-production/

Тестинг: https://deploy.yandex-team.ru/stage/passport-uaas-proxy-testing/

#### Графики
Прод: https://yasm.yandex-team.ru/chart/itype=passportuaasproxy;hosts=ASEARCH;ctype=production;signals=unistat-uaas.success_dmmm,diff(unistat-uaas.total_dmmm,unistat-uaas.success_dmmm)

Тестинг: https://yasm.yandex-team.ru/chart/itype=passportuaasproxy;hosts=ASEARCH;ctype=testing;signals=unistat-uaas.success_dmmm,diff(unistat-uaas.total_dmmm,unistat-uaas.success_dmmm)

#### CI
https://a.yandex-team.ru/projects/passp/ci/releases/timeline?dir=passport%2Fpython&id=passport-uaas-proxy-release

#### ABC
https://abc.yandex-team.ru/services/passp-uaas-proxy/

### Генерация easyjson
Если аркадия примонтирована к `~/gopath/src/a.yandex-team.ru`:

`ya make ~/gopath/src/a.yandex-team.ru/vendor/github.com/mailru/easyjson/`

`GOPATH=~/gopath ~/gopath/src/a.yandex-team.ru/vendor/github.com/mailru/easyjson/easyjson/easyjson uaas/client_uaas.go`

### Интерфейс (параметры в ручку)
Параметры формы:
- `test_ids` - test-id через запятую, которые надо вернуть, для отладки
- `device_id` - по этому параметру происходит разделение экспериментов
- `real_ip` - айпишник, который будет передан в uaas
- `app_id` - по этому параметру происходит переписывание экспериментов

Заголовки:
- `X-Yproxy-Header-Ip` - его проставляет укропрокси
- `Ya-Consumer-Client-Ip` - его проставляет nginx
