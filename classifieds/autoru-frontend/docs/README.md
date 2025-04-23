# Документация

## Основное
* [Первые шаги, основы работы с проектом](./first-steps.md)
* [Дежурство](./duty.md) - обязанности дежурного и инструкции к действию
* [Логи](./grep-logs.md) - как смотреть и грепать логи
* [Код-ревью](./code-review.md) - описание процесса ревью кода
* [Как мы делаем фичи](./workflow.md) - верхнеуровневое описание этапов жизненного цикла задачи от появления идеи до релиза функциональности
* [Contribution](./contribution.md) - как вносить изменения в проект, описание этапов работы над задачей с точки зрения разработчика
* wiki [Как мы работаем с дизайнерами](https://wiki.yandex-team.ru/verticals/frontend/dsgnfront/)

## Главное по разработке
* [React Codestyle](./react-codestyle.md)
* [React и нейминг](./react-naming.md)
* [CSS](./css.md) - как мы пишем css в деталях: работа с цветами, типографикой, вложенностью и БЭМ.
* [Descript](./descript.md) - как мы используем внутренний фреймворк агрегации запросов на сервере, какие сущности создаем и куда складываем файлы.

## Деплой и релизы
* [О сборке и деплое](./build-and-deployment.md) - общие сведения о том, как устроена сборка и процесс деплоя
* [Правила проведения релизов](./RELEASE.md), справедливые для всех проектов

## Тесты
* [Юнит-тесты с Jest](./jest-cookbook.md) - подробная инструкция по написанию тестов с примерами, включая снепшотное тестированиие и способы замокать разные сущности.
* [Браузерные тесты с Jest и Puppeteer](./jest-puppeteer-react.md) - инструкция по написанию бразуерных тестов для проверки верстки компонентов. Подготовка, область применения, примеры, запуск и дебаг тестов.

## Здоровье сервисов
* [Система мониторинга](./monitoring.md) - список всех актуальных дашбордов в Grafana, описание основ работы нашей системы мониторинга, полезные советы, инструкции по работе с метриками и их добавлению
* ext [CSP отчёты](https://csp.yandex-team.ru/projects/auto_ru/projectDashboard)
* wiki [Что такое CSP](https://wiki.yandex-team.ru/product-security/csp/)

## Доки по работе с сервисами
* [Команды для работы с всеми сервисами](./commands.md)
* [`www-autoru-yandex`](../www-autoru-yandex/Readme.md)
* [`www-cabinet`](../www-cabinet/README.md)
* [`www-callmen`](../www-callmen/Readme.md)
* [`www-mag`](https://wiki.yandex-team.ru/vertis-traffic-interfaces/mag-autoru/)
* [`www-printer`](../www-printer/README.md)
* [`www-search-app-updater`](../www-search-app-updater/README.md)
* [`www-search-app`](../www-search-app/README.md)
* [`www-url`](../www-url/Readme.md)

## Полезно знать
* [MDS S3](./mds-s3.md)
* [Protobuf](./protobuf.md)
* [SVG иконки](./react-svg.md) - куда складывать svg иконки, как их добавлять и использовать
* [Бункер](./bunker.md) - что такое бункер и как с ним работать
* [Гео-данные](./geo.md)
* [Логирование с клиента](./client-to-server-logs.md): как записать что-то в лог с клиента на сервер, грепать лог и с какой частотой это можно делать
* [Реклама](https://a.yandex-team.ru/arcadia/classifieds/vertis-frontend/packages/ads) - всё про работу рекламы в Вертикалях: принцип, ручки, конфиги
* [Роутинг и генерация ссылок](./router.md)
* [Секретница](./secrets.md) - как пользоваться секретницей и добавлять новые секреты
* [Таймауты и ретраи](./backend-timeouts.md) - зачем нужны таймауты для запросов в бекенды, как правильно подобрать значение и нужны ли ретраи
* [Эксперименты](./user-experiments.md)
* wiki [Proof of Work](https://wiki.yandex-team.ru/verticals/frontend/proof-of-work-usage/)
* wiki [Как сравнить клиентские метрики скорости релиза с продом](https://wiki.yandex-team.ru/verticals/frontend/verticals-testing-speed-teamcity/)

## Разное
* [Версии Node.js и их обновление](./how-to-update-nodejs.md)
* [Запуск e2e тестов в бранче, выкатка ветки в бранч](./e2e-test-in-branch.md)
* [Как дебажить docker-контейнер](./how-to-debug-docker-container.md)
* [Кладбище проектов](./graveyard.md) - некоторые из проектов, которые мы хоронили и когда это было сделано
* [Конфиги nginx](./nginx-cong.md)
* [Микроразметка](./schema_org.md)
* [Полезности и лайфхаки](./tips-and-tricks.md) (но пока их мало)
* [Работа с чатиком](./www-chat/README.md) - где живет чат, который используется на Авто.ру, как его собирать и работать с ним
* [Работа с легаси кодом i-bem](./how-to-bem.md)
* [Редакторы кода](./editor.md) - выбор редактора кода, советы, лайфхаки, полезные расширения
* [Синк кода с виртуалкой через realsync](./realsync.md)
* [Статика](https://a.yandex-team.ru/arcadia/classifieds/yandex-vertis-autoru-static) - где лежит и как релизить статику
* wiki [AMP](https://wiki.yandex-team.ru/verticals/frontend/amp/)
* wiki [Доступ к данным из MySQL](https://wiki.yandex-team.ru/vertis-admin/storage/mysql/dev/) - админская документация, описывающая получение доступа к базе данных в тестинге
* wiki [Серверы в тестовой среде](https://wiki.yandex-team.ru/autoru-dev/Testing/vastutnestoyalo/)
