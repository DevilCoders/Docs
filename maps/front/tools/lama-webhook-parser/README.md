# lama-webhook-parser

Рантайм вебхука для публикации lama.yaml конфигов.

**Схема работы:**
1. GitHub отправляет вебхук на push-event в репозитории в `https://podrick.c.maps.yandex-team.ru/github/lama-webhook`
2. Подрик [обрабатывает](https://github.yandex-team.ru/maps/podrick-int/blob/master/server/projects/github/lama-webhook.js) вебхук.
3. Если в списке добавленных/измененных файлов содержится `lama.yaml` конфиг — запускается [реакция](https://reactor.yandex-team.ru/browse?selected=8466202), которая содержит в себе этот пакет.
4. Пакет парсит вебхук и собирает конфиги, которые нужно опубликовать.
5. `lama sync -f -r --directory ./configs`