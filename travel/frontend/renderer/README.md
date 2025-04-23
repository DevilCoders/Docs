# Renderer

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/renderer&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/renderer)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/renderer&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/renderer)

Сервис для отрисовки писем по данным.
Использует разметку [mjml](https://mjml.io/documentation/)

Построено на основе [core](https://ui.yandex-team.ru/)

### Структура

-   `controllers` - контроллеры для точек входа. Занимаются разбором параметров и взаимодействием с объектами запроса/ответа
-   `services` - логика по отрисовке писем
-   `blocks` - содержит модули соответсствующие блокам в дизайне + набор моков для тестирования
-   `components` - кастомные компоненты для mjml

### Роуты

-   `/` - основной роут для `POST` запросов, получает массив блоков `{type, data}`, возвращает соответствующую вёрстку
-   `/test` - `GET` роут для тестирования писем. По-умолчанию выводит все блоки со всевоозможными комбинациями входных данных. Для того чтобы отобразить только какой-то определённый тип блоков можно использовать параметр `type` - `/test?type=header&type=footer`

### Типы блоков

`TODO: добавить после разработки спеки`

### Deploy

-   [Deploy](https://deploy.yandex-team.ru/projects/travel-frontend-renderer)

### Testing

https://travel-tools-test.yandex.net/renderer/

[Балансировщик](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/show/)

### Production

https://travel-tools.yandex.ru/renderer/

[Балансировщик](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-internal-balancer/show/)

## Мониторинги и дашборды

[Дашборд](https://datalens.yandex-team.ru/huurcsd89uwse-travel-frontend?tab=yZa)

| Мониторинг     | Production                                                                                              |
| -------------- | ------------------------------------------------------------------------------------------------------- |
| **5xx ошибки** | [Настроить](https://yasm.yandex-team.ru/alert/travel_frontend_renderer_production_response_5xx_ydeploy) |
