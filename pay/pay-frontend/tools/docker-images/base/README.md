# Веб-сервис

Базовый образ для поднятия финтех-сервиса на Duffman'e.

`registry.yandex.net/yandex-pay/frontend/base:stable`.


## Настройка смежных сервисов перед запуском

#### Логброкер
Настроить топики:
- `<topic-prefix>-access-log` — для логов Nginx
- `<topic-prefix>-duffman-log` — для логов Duffman'a


## Настройка сервиса

#### Настроить ENV переменные
- `WEB_SERVICE_ENV` — `production` / `testing` / `development` 
- `LOGBROKER_TOPIC` — префикс для топиков логброкера
- `DUFFMAN_BASEPORT` — базовый порт для Duffman'a (укажите 8080)
- `DUFFMAN_WORKERS` — количество воркеров (обычно кратно CPU)
- `SECRET_KEY_PEM` — приватный SSL ключ
- `SECRET_CERT_PEM` — SSL сертификат 


#### Nginx
Для настройки Nginx можно перекрыть след. конфиги:

Конфиги в `/etc/nginx/sites-available/`.

Нужно настроить для запуска сервиса
- `web-service-locations-static.include` — локейшены для Статики

Лучше не трогать если точно не понимаете зачем вам это: 
- `web-service.conf` — корневой конфиг
- `web-service-backend.include` — настройка upstream до воркеров Duffman'а
- `web-service-locations-proxy.include` — локейшены для проксирования к Duffman'у
- `web-service-ssl.include` — настройки SSL (важно соблюсти пути)
- `web-service-directives.include` — общие настройки Nginx


#### Исходники Duffman-сервера

Предполагается что сервер на TypeScript.  
Должны быть соблюдены пути:
- `/usr/src/web-service` — кореневая папка сервера
- `/usr/src/web-service/node_modules` — зависимости в т.ч. и Duffman
- `/usr/src/web-service/dist` — скопмилированный TypeScript


## Запуск в Deploy

Все сервисы внутри контейнера запускаются через supervisor.

Ворклоады `/opt/workloads`
- `supervisor-start.sh` — запускает сервисы
- `supervisor-check.sh` — внешняя проверка запущеных сервисов

**Если нужно запустить сервисы при старте контейнера**  
Нужно добавить в контейнер `/opt/entrypoint.sh`
```bash
source /opt/workloads/supervisor-start.sh
```

## Пример Dockerfile'a

```Dockerfile
FROM registry.yandex.net/yandex-pay/frontend/base:stable

# Nginx static locations 
COPY fs/web-service-locations-static.include /etc/nginx/site-available

# Copy Duffman server
COPY src  /usr/src/web-service/src
COPY .npmrc \
     package.json \
     package-lock.json \
     tsconfig.json \
     /usr/src/web-service/


RUN && apt-get update \
    # Зависимости для компиляции node-биндингов
    # Они нужны только для компиляции и ниже мы их убираем
    && apt-get install -y -q --no-install-recommends --no-install-suggests build-essential \
    \
    && cd /usr/src/web-service \
    && npm run deps \
    && npm run compile \
    \
    && apt-get remove --purge --auto-remove -y build-essential \
    && rm -rf /var/lib/apt/lists/*
```
