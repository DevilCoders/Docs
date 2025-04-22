# Документация монорепозитория frontend

## Описания устройства

- [Профиты от жизни в монорепозитории](./faq/profits.md)
- [Требования монорепозитория frontend](./faq/requirements.md)
- [Гарантии в монорепозитории со стороны инфраструктуры](./faq/sla.md)
- [Набор готовых решений](./faq/solutions.md)
- [Какие общие проверки есть в монорепозитории?](./faq/checks.md)
- [Units](./faq/units.md)
  - Различия в запуске в PR/MQ/транке
- [Линтеры в монорепозитории](./faq/linters.md)
  - Локальный запуск
  - husky + lint-staged в проекте
- Какие интеграции с инфраструктурными сервисами есть в монорепозитории?
    - Инструмент для кодревью – [devexp](https://github.yandex-team.ru/devexp/devexp)
    - Сервис для автоматического вливания пулл-реквестов - [Merge Queue](https://github.yandex-team.ru/search-interfaces/microservices/tree/master/services/merge-queue) позволяет организовать green trunk, интеграционно протестировать изменения на обязательных проверках.
- [Автопубликация новых версий npm-пакетов при влитии PR-а](./faq/packages-autopublish.md)
- [Как работают сборка и выкладка на бету](./faq/prepare-beta.md)?
- [Как работать с зависимостями?](./faq/dependencies.md)
    - Коммитить ли изменения в package-lock.json?
    - Как контролировать версии зависимостей?
- [Как работает стек Apphost + Report Renderer](./faq/introduction-to-apphost-and-rr.md)?
- [Как устроен релизный процесс сервисов](./faq/release-workflow.md)?
- [Как работает форма для релизов](./faq/release-form.md)?
- [Зачем Publish MQ Artifacts](./faq/publish-mq-artifacts.md)

## Руководства

- [Cоздать новый лист](./how-to/create-new-leaf.md)
- [Чеклист для запуска нового сервиса](./how-to/check-list.md)
- [Мигрировать git-репозиторий в монорепозиторий](./how-to/import/from-git.md)
- [Мигрировать с Drone CI](./how-to/migrate/from-drone.md)
- [Собрать статику для библиотеки или сервиса](./how-to/static.md)
- [Мигрировать сервис на стек Apphost + Report Renderer](./how-to/migrate-to-apphost-and-rr.md)
- [Настроить перевод статуса задачи после вливания пулл-реквеста](./how-to/change-ticket-status.md)
- [Генерировать описание пулл реквеста](./how-to/generate-pr-description.md)
- [Настроить селективность в проекте](./how-to/selectivity.md)
- [Посмотреть билд в транке после мержа ревью-реквеста](./how-to/find-trunk-build.md)

### Проверки в CI

- [Завести новую проверку в CI](./how-to/checks-introduction.md)
- [Настроить Pulse](./how-to/setup-pulse.md)
- [Мониторинг CI/CD](https://doc.yandex-team.ru/si-infra/deprecated-ci-monitoring.html)

### Тестирование

- [Настроить тестирование своего сервиса с помощью асессоров](./how-to/crowdtesting-from-pr.md)
- [Подключить генерацию эксперимента для залипания в шаблоны беты на продакшене](./how-to/experiment-sticky.md)
- [Подключить возможность запускать hermione под флагами](./how-to/hermione-exp-flags.md)
- [Подключить подсчет диффа покрытия в ПРе](./how-to/coverage/unit.md)
- [Подключить подсчет покрытия в hermione](./how-to/coverage/hermione.md)

### Релизы

- [Настроить релизы сервисов](./how-to/setup-releases.md)
- [Настроить деплой RR-шаблонов в продакшен](./how-to/deploy-rr-templates-to-production.md)
- [FAQ по релизам](./faq/release.md)

### Выезд из монорепозитория frontend
- [Инструкция](https://wiki.yandex-team.ru/search-interfaces/infra/arcadia/leave-monorepo/diy/)
