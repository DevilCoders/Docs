# Окружения для разработки и тестирования, и продакшн

## Hamster

Балансеры: [AWACS hamster](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hamster.yandex.ru/upstreams/list/upstream_shared_hamster_jobs_test/show/), [AWACS vacancies-testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/vacancies-testing/show/)

- https://hamster.yandex.ru/jobs

Специальное окружение для проверки изменений с тестовыми данными.
Отражает текущий продакшн, но позволяет подменять источники (походы в бекенды): например, позволяет подменить поход в Фемиду или LPC. Или граф целиком для отладки и внесения в него изменений. В LPC по умолчанию ходит с флажком preview (в неопубликованные данные).
Это наш стабильный тестинг.

Управлять походами позволяют [CGI-параметры srcrwr, graph](https://docs.yandex-team.ru/apphost/pages/cgi#srcrwr), и другие (См. [Архон и локальная разрботка](./archon.md)).

| Зависимость | Значение | Переопределение |
|-------------|----------|-----------------|
| Граф | прод | graph=<нужный граф> |
| Фемида | тест | - |
| LPC | прод, неопубликованный | set_prod=true |

На базе него с помощью параметров и сервиса [stoker](https://stoker.z.yandex-team.ru/matches) (введите jobs для просмотра) «созданы» все другие тестовые окружения и стенды: 1) фиче-стенды, 2) стенд для транка, 3) приёмка.

### srcrwr
- Открыть hamster с локальным turbo: [на соседней странице](./archon)
- Открыть hamster с конкретным стендом бека фемиды: добавить query параметр `srcrwr=FEMIDA_TEST_EXTERNAL:<femidaStandAddress>` к примеру `srcrwr=FEMIDA_TEST_EXTERNAL:https://hallucinite.femida.test.yandex-team.ru:443`

### Фиче-стенды (бетки) и стенд для транка

Создаются на каждый пулл-реквест в сервис jobs.

- https://renderer-jobs-dev.hamster.yandex.ru/jobs
- `https://renderer-jobs-pull-${pull_request_id}.hamster.yandex.ru/jobs`

### Приёмка

- https://rctemplates-jobs.hamster.yandex.ru/jobs/

Служит для принятия изменений в «шаблонах» (функуциях и компонентах). На него робот автоматически выкатывает приложение при создании релизного тикета при попытке релиза шаблонов.

## Продакшн

- https://yandex.ru/jobs/

Балансеры: [knoss_fast](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast/upstreams/list/?filter=%7B%22idRegexp%22:%22jobs%22%7D), [AWACS vacancies](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/vacancies/show/)

> NB: Создавать апстримы в knoss_fast мы сами не можем, нужно создавать тикет в очередь MINOTAUR по образу и подобию https://st.yandex-team.ru/MINOTAUR-2759

| Зависимость | Значение | Переопределение |
|-------------|----------|-----------------|
| Граф | прод | graph=<нужный граф> |
| Фемида | прод | - |
| LPC | прод, опубликованный | - |

### l7test (препродакшн)

- https://l7test.yandex.ru/jobs/

Балансеры: [knoss_fast_testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/upstreams/list/?filter=%7B%22idRegexp%22:%22jobs%22%7D), [AWACS vacancies](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/vacancies/show/).

В этом окружении работают контент-менеджеры.

| Зависимость | Значение | Переопределение |
|-------------|----------|-----------------|
| Граф | прод | graph=<нужный граф> |
| Фемида | прод | - |
| LPC | прод, неопубликованный | - |
