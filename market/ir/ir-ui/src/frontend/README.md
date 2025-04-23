Фронтенд часть
==============

Процесс разработки в Аркадии:
1. При изменениях в `package-lock.json` нужно запустить скрипт `./update-arcadia-resources.sh`. !!**ВАЖНО вкоммитеть эти изменения**!!
2. При добавлении новых файлов в корень, которые должны быть доступны сборке, нужно обновлять:
  - `./ya.make`, в `JAVA_SRCS`
  - `../frontend-static`, после `--frontend-sources`
3. Как сгенерировать `src/rest/definitions.ts` из Java:
  - запустить `scripts/run-frontend.sh` в корне проекта
  - по сути - `ya make` в этой папке + `unzip -o ir-ui-frontend-sources.jar srс/rest/definitions.ts`

# Проксирование запросов на тестовый/боевой сервер

1. Скопируйте `cp .env.local.sample .env.local`
2. Укажите хост на кторый нужно проксировать запросы в параметр PROXY_HOST

