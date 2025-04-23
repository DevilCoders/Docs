# Lenour release runner?
Сервис для запуска рецепта раскатки шаблонов через Ленор. Находит ID целевого ресурса и делет коммит в релизную ветку.

## Использование

В [мета-рецепте nanny](https://wiki.yandex-team.ru/runtime-cloud/nanny/dashboards/metarecipes-ui/) добавить кубик http_request с адресом `http://lenour-release-runner.si.yandex-team.ru/` и GET-параметром prj (для веба `prj=web`).

## Как собрать?

  * `npm i`
  * `npm run build`

## Как запустить?

  * `npm start -- -p 3000`

## Как разрабатывать?

  * `npm run watch`

## Как собрать Docker-образ?

  * `npm run docker-build`

## Как запустить Docker-образ?

  * `npm run docker-build`
  * `RUN_ARG="-p 3000:80 -e NANNY_TOKEN=<NANNY_TOKEN> -e ARCANUM_OAUTH_TOKEN=<ARCANUM_OAUTH_TOKEN>" npm run docker-run`
  * `curl http://localhost:3000`

  Токен nanny можно получить [тут](https://nanny.yandex-team.ru/ui/#/oauth/).
  Токен arc можно получить [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5c407aafc5c242948b532842a9a07da6).

## Сертификаты
В переменной окружения `NODE_EXTRA_CA_CERTS` должен быть указан путь к сертификату `YandexInternalRootCA.crt`.
В докер-образ сертификат подкладывается на этапе сборки. Для локальной разработки cертификат можно скачать по [ссылке][https://crls.yandex.net/YandexInternalRootCA.crt].

## Доступы
Для работы сервиса нужен доступ к `api.arc-vcs.yandex-team.ru:6734` (gRPC API арка), доступ до `nanny.yandex-team.ru:443` (Nanny API).

## Сетевые макросы сервиса
Сервис живет в [_LENOUR_RELEASE_RUNNER_NETS_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_LENOUR_RELEASE_RUNNER_NETS_).

## Как обновить образ?

  Влить изменения в dev. Будет автоматически выпущена новая версия. После этого в trunk выполнить

  * `npm run docker-publish`
  
  Зайти на сервис `https://deploy.yandex-team.ru/stage/lenour-release-runner` и обновить docker-образ для сервиса.

## Где запускается проект

  * `https://deploy.yandex-team.ru/stage/lenour-release-runner`
  Поддержкой сервиса занимается команда [Report Renderer Development](https://abc.yandex-team.ru/services/reportrenderer/)
