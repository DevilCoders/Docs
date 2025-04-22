# Служба инфраструктуры поисковых интерфейсов

Наша миссия — создать условия для того, чтобы разработчики фронтенда в Яндексе могли быстрее и удобнее разрабатывать и доставлять фичи в продакшен.

[Дежурство](https://wiki.yandex-team.ru/infraduty) • [Демо](https://wiki.yandex-team.ru/infrademo) • [Вики](https://wiki.yandex-team.ru/search-interfaces/infra) • [Исходный код данной документации](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/fei-docs)

## Наши инструменты

### Для продакшена

- [Report Renderer](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/) – сервис для запуска JavaScript под AppHost; поставляется вместе с инфраструктурой вокруг релизов, мониторингов и т.п.
- [ApphostLib](https://docs.yandex-team.ru/apphost/pages/api_nodejs) – библиотека для разработки произвольных аппхостовых источников на JavaScript и TypeScript.

### Для локальной разработки

- [Kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html) — сервер локальной разработки, который берёт на себя работу с AppHost и передаёт данные в Report Renderer. Позволяет сохранять и воспроизводить дампы ответов AppHost-источников, что удобно для тестирования.
- [Archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html) — cli-инструмент для запуска произвольных команд, в том числе для лёгкого поднятия окружений локальной разработки. Позволяет делать свои cli и описывать запускаемые процессы в виде графа.
- [Clement](https://doc.yandex-team.ru/si-infra/local_devserver/clement.html) — nodejs-приложение для записи и воспроизведения HTTP запросов. Позволяет сохранять и воспроизводить дампы для hermione-тестов, если вы не на apphost-стеке.
- [Tunneler](./tunneler/tunneler.md) — сервис, предоставляющий HTTPS over SSH туннели. Позволяет сделать доступным ваше локальное приложение с других устройств во внутренней сети Яндекса.
- [Проверки счетчиков и метрик качества](./counters-and-metrics/structure.md) — набор инструментов, позволяющий при локальной разработке и тестировании проверять корректность срабатывающих счетчиков и вычисляемых метрик.

### Для автоматического тестирования

- [Hermione](https://doc.yandex-team.ru/si-infra/hermione/hermione.html) - инструмент для интеграционного тестирования, прозволяющий автоматизировать тестирование пользовательских сценариев в браузере. Под капотом используется библиотека [wdio](https://webdriver.io/) и интерфейс [mocha](https://mochajs.org/) для написания тестов. Для гермионы уже написан ряд плагинов (см. раздел [hermione:плагины](https://doc.yandex-team.ru/si-infra/hermione/hermione.html)), позволяющих удобно разрабатываться и писать тесты на внутреннем стеке.
- [Testcop](https://doc.yandex-team.ru/si-infra/stabilnost_testov_skipy_myuty_statistika/testcop/testcop.html) - сервис для работы с нестабильными тестами в hermione. Предоставляет как интерфейс для ручного отключения нестабильных тестов, так и автоматику по мьюту (тесты прогоняются, но не влияют на результат сборки) таких тестов без участия разработчика.
- [Тестирование под флагами](https://a.yandex-team.ru/arc_vcs/frontend/docs/how-to/hermione-exp-flags.md) — набор инструментов для ручного запуска hermione-тестов под флагами.
- [SurfWax](https://wiki.yandex-team.ru/surfwax/) — динамический Selenium Grid. Самостоятельно поднимает браузеры под нагрузку, экономит таким образом железо. Предоставляет интерфейсы WebDriver и Chrome DevTools Protocol, с которыми умеют работать множество клиентов и тестраннеров. Сейчас ОЧЕНЬ WIP.

### Для ручного тестирования

- [TestPalm](https://abc.yandex-team.ru/services/tms) — система управления тестированием, реализущая хранение, управление и агрегацию тест-кейсов с возможностью их последующего запуска раздачи заданий на асессоров.
- [palmsync](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/palmsync) — инструмент для валидации тестовых сценариев сервиса и их синхронизации в проект TestPalm для последующего прохождения руками тестировщиков, асессоров или толокеров.
- [Crowdtest Runner](https://wiki.yandex-team.ru/search-interfaces/infra/crowdtest/create-launch) — сервис запуска раздачи заданий на асессоров или толокеров, предоставляющий слой интеграций с [Я.Краудтестирование](https://wiki.yandex-team.ru/crowdtesting).
- [testpalm-suite-runner-cli](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/testpalm-suite-runner-cli) — инструмент для создания и запуска тест-ранов в TestPalm из заранее сконфигурированных тест-сьютов с возможностью их предварительной валидации и условного запуска.
- [expflags-cli](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/expflags-cli) — инструмент синхронизации деклараций флагов, хранящихся рядом с кодом сервиса, в AB Flags Storage, чтобы не создавать и обновлять флаги вручную.
- [testid-cli](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/testid-cli) — инструмент создания выборок (testid) на основне используемых флагов в тест-кейсах и ссылок на залипание для бет пулл-реквестов.
- [Релизы с экспериментальными флагами](https://abc.yandex-team.ru/services/releases-expflags) — набор инстументов, предоставляющих возможность запуска других инструментов для проверки сервиса под экспериментальными флагами.

### Для CI/CD

- [Merge Queue](https://a.yandex-team.ru/arc_vcs/frontend/projects/microservices/services/merge-queue/README.md) — сервис для автоматического вливания пулл-реквестов для организации green trunk. Позволяет ловить интеграционные баги и настраивать обязательные проверки.
- [Селективность](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/selectivity/README.md) — инструмент, позволяющий описать зависимости проверок в ci от измененных файлов. Благодаря ему можно не запускать лишние проверки в конвейере. Например, не запускать тесты при изменении документации.
- [Checks Skipper](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/checks-skipper/README.md) — сервис для мьюта обязательных проверок в CI.
- [prosperity](https://a.yandex-team.ru/arc_vcs/frontend/projects/microservices/services/prosperity/README.md) — набор хуков для интеграции GitHub и Arcanum с Трекером. Сокращает количество ручной работы по ведению и оформлению тикетов и пулл-реквестов.
- [Релизные процессы](https://abc.yandex-team.ru/services/32419) — набор sandbox тасок для релиза собранного ресурса с шаблонами, cli на js для отведения релизов и вебхуков для упрощения выкладки релиза на приёмку и отправки на продакшен.
- [Sandbox-CI](https://abc.yandex-team.ru/services/sandbox-ci/) — (поддерживается, не развивается) — CI/CD для фронтенд проектов на базе Sandbox.
- [Trendbox-CI](https://doc.yandex-team.ru/si-infra/trendbox_ci/trendbox_ci.html) (поддерживается, не развивается) — CI/CD для фронтенд проектов.
- [Castle](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/castle/README.md) - утилита для запуска конкретных ci-проверок на локальных изменениях без создания пулл-реквеста. На данный момент работает только для sandbox-ci.

### Для наблюдения

- [Графики Cycle Time](https://wiki.yandex-team.ru/search-interfaces/infra/charts/cycletime/) — дашборд, позволяющий оценить скорость разработки и найти бутылочные горлышки в вашем процессе. Основан на данных Трекера.
- [Графики налоговых целей (SLA, КГБ, TimeSpent)](https://wiki.yandex-team.ru/search-interfaces/infra/crowdtest/chart-docs) — набор графиков, позволяющих отслеживать продвижение по налоговым целям.
- [Автоподсчёт приоритета багов](https://a.yandex-team.ru/arc_vcs/frontend/projects/microservices/services/assessors/routes/tracker/calculate-priority/docs/README.md) — сервис автоматического расчёта приоритета багов на основе различных данных, включая кастомные поля в Трекере, число пользователей по счётчикам и ErrorBooster.

### Другое

- [Беты шаблонов на report-renderer](https://doc.yandex-team.ru/si-infra/renderer-betas/general.html) — сервис для подмены стабильной версии шаблонов для report-renderer на бета-версию в преимущественно тестовых окружениях, таких как hamster.
- [Foreverdata](https://wiki.yandex-team.ru/search-interfaces/infra/infratools/services/foreverdata/) — сервис для быстрой подмены данных на поисковой выдаче. Позволяет сохранить дамп данных данных для фичи и показывать её на вёрстке под специальным cgi-параметром.Например, если заморозить сниппет на первой позиции, то при запросе с параметром на первом месте всегда будет показываться этот сниппет, а остальная выдача будет живая.
- [YFrame](https://abc.yandex-team.ru/services/yframe) - сервис для ручного просмотра фич на серпе по свежим запросам, полученным по счетчикам показа (blockstat/baobab) этих фич.
- Поддержка Node.js и TypeScript в [ya make](https://wiki.yandex-team.ru/yatool/make/) — возможность собирать проекты на TS стандартными средствами Аркадии. Даёт интеграции с распределённой сборкой, с NewCI, с протобуфами и другими общими инструментами. Сейчас ОЧЕНЬ WIP.
- [Тасклеты](https://wiki.yandex-team.ru/sandbox/tasklets/) на TypeScript — возможность разрабатывать собственные тасклеты на TS. Позволяет, например, сделать свои кубики для NewCI на TS. Сейчас ОЧЕНЬ WIP.
