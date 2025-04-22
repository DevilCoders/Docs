Фронтенд часть
==============

### Запуск проекта

При первом запуске приложения, в файл `/etc/hosts` (`C:\Windows\System32\Drivers\etc\hosts` - для Windows) необходимо добавить следующие записи (это необходимо сделать только один раз):

```
127.0.0.1   localhost.msup.yandex-team.ru
127.0.0.1   localhost.msup.yandex.ru
```

Далее устанавливаем зависимости:

```bash
npm ci
```

Запускаем приложение:

```bash
npm start
```

### Процесс разработки в Аркадии:

1. При изменениях в `package-lock.json` нужно запустить скрипт `./update-arcadia-resources.sh`. !!**ВАЖНО вкоммитеть эти изменения**!!
2. При добавлении новых файлов в корень, которые должны быть доступны сборке, нужно обновлять:
  - `./ya.make`, в `JAVA_SRCS`
  - `../frontend-static`, после `--frontend-sources`
3. Как сгенерировать `src/rest/definitions.ts` из Java:
  - запустить `scripts/run-frontend.sh` в корне проекта
  - по сути - `ya make` в этой папке + `unzip -o ir-ui-frontend-sources.jar srс/rest/definitions.ts`

### Проксирование запросов на тестовый/боевой сервер

1. Скопируйте `cp .env.local.sample .env.local`
2. Укажите хост на кторый нужно проксировать запросы в параметр PROXY_HOST
