Фронтенд часть
==============

Процесс разработки в Аркадии:
1. При изменениях в `package-lock.json` нужно запустить скрипт `./update-arcadia-resources.sh`. !!**ВАЖНО вкоммитеть эти изменения**!!
2. При добавлении новых файлов в корень, которые должны быть доступны сборке, нужно обновлять:
  - `./ya.make`, в `JAVA_SRCS`
  - `../frontend-static`, после `--frontend-sources`
3. Как сгенерировать `src/rest/definitions.ts` 
  -  в package.json есть команда `generate:definitions` простозапускаем ее

  генерация другими путями:
  - запустить `scripts/run-frontend.sh` в корне проекта
  - по сути - `ya make` в этой папке + `unzip -o ir-ui-frontend-sources.jar srс/rest/definitions.ts`

# Проксирование запросов на тестовый/боевой сервер

1. Скопируйте `cp .env.local.sample .env.local`
2. Укажите хост на кторый нужно проксировать запросы в параметр PROXY_HOST

Для проксирования запросов можно использовать следующие хосты:

- https://ct-testing.market.yandex.ru/ - тестинг
- https://ct.market.yandex.ru/ - прод


# Атопроставление кук 

За это отвечает либа @yandex-int/magicdev

1. В файл `/etc/hosts` (`C:\Windows\System32\Drivers\etc\hosts` - для Windows) добавить следующие записи:

```
127.0.0.1   localhost.msup.yandex-team.ru
127.0.0.1   localhost.msup.yandex.ru
```

2. "Нарезать" сертификат и приватный ключ и положить их в директорию ssl.local:

```bash
mkdir ssl.local
sed -n '/-----BEGIN PRIVATE KEY-----/,/-----END PRIVATE KEY-----/p' node_modules/@yandex-int/magicdev/data/yandex.pem > ssl.local/yandex.key
sed '/-----BEGIN PRIVATE KEY-----/,/-----END PRIVATE KEY-----/d;/^\s*$/d' node_modules/@yandex-int/magicdev/data/yandex.pem > ssl.local/yandex.crt
touch .env.local
echo 'SSL_CRT_FILE="ssl.local/yandex.crt"' >> .env.local
echo 'SSL_KEY_FILE="ssl.local/yandex.key"' >> .env.local
```