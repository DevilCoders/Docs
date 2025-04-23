# Карьерный портал (Сайт Вакансий)

Продакшн:
- https://yandex.ru/jobs
- https://yandex.com/jobs

[Схема работы КП СВ](https://miro.com/app/board/o9J_lKGmgU4=/), [подробная документация](./docs/index.md)

## Быстрый старт

1. `nvm use`
2. `npm i`
3. `npm run build`
4. `npm start`

## Общая информация

Сайт вакансий работает под [Apphost](https://docs.yandex-team.ru/apphost/). Данные получает из: [Фемиды](https://femida.yandex-team.ru) и [Конструктора](https://lpc.yandex-team.ru/jobs).

Вертикаль сайта вакансий называется [JOBS](https://horizon.z.yandex-team.ru/verticals/JOBS/Info), [продакшн-граф в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/JOBS/jobs.json) лежит в директории вертикали. Визуальное представление графа - [в Horizon](https://horizon.z.yandex-team.ru/graphs/svg/JOBS/jobs/_/trunk).

## Стенды и окружения

- [`hamster`](https://hamster.yandex.ru/jobs) — специальное разработческое окружение, базовое для остальных (см. [hamster](https://docs.yandex-team.ru/apphost/hamster))
- [стенды jobs](https://renderer-jobs-dev.hamster.yandex.ru) — окружения с RR-шаблонами из фиче-веток и мастера
- [`priemka` для шаблонов](https://rctemplates-jobs.hamster.yandex.ru/jobs) — окружение для тестирования контента перед раскаткой в продакшн
- [`l7test`](https://l7test.yandex.ru/jobs) — окружение для тестирование контента (см. [l7test](https://docs.yandex-team.ru/apphost/hamster#l7test))
- [`production`](https://yandex.ru/jobs) — продакшн окружение

## Разработка

Есть 4 части: конфигурация аппхоста (граф), функции-«миддлвары» (этот репо), отображающая часть (turbo), админская часть (lpc). И [API Фемиды](https://a.yandex-team.ru/arc_vcs/intranet/femida/src/api), откуда мы забираем данные.

При необходимости есть возможность локально поднять и связать сервисы Jobs, Турбо, и LPC (см. [hamster](https://docs.yandex-team.ru/apphost/hamster)).

### Графы

Описывают правила похода в источники (бекенды) и обработки запроса пользователя.

Редактировать [локально](./graphs/testing.json) и в [Horizon](https://horizon.z.yandex-team.ru/graphs?arcpath=UI&vertical=JOBS) (тэг UI).

### Функции

Несколько источников в графе обслуживаются RR с JS-функциями, которые работают с контекстом AppHost и [лежат в этом репозитории](./src/entries/server): router, merger, responder, и другие. Полный список используемых функций в [конфигурации для RR](./routes.json).

### Компоненты для отображения контента ([Turbo](https://a.yandex-team.ru/arc_vcs/frontend/services/turbo))

[Визуальная часть](https://turbo-docs.in.yandex-team.ru/story/dev/?path=/story/lcjobs-header--default) располагается в сервисе Turbo, PRы можно делать одновременно с изменениями в функциях.

Не забывайте делать Стори в Сторибуке для компонентов с префиксом `LcJobs*`.

### Переводы

Большая часть переводов у нас лежит в [турбо](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/turbo). Обновляются они через [танкер](https://tanker.yandex-team.ru/project/turbo?branch=master) с помощью tanker-kit.

`npx tanker push path/to/component/component.i18n` – для пуша в танкер.
`npx tanker sync path/to/component/component.i18n` – для синка.

`component/component.i18n` – правильное название папки, иначе переводы не будут найдены

[Доп инфа по tanker-kit](https://wiki.yandex-team.ru/search-interfaces/tanker/tanker-kit/#rabotastanker-kit).

Пометка: когда используешь sync можно обновляется `.../component.i18n/index.ts`, где бывает определение функции `translations`:

```
import i18n from '@yandex-int/i18n';

import { en } from './en';
import { ru } from './ru';

export const translations = i18n({ ru, en });
```

Помимо переводов в турбо, у нас есть переводы в [lpc](https://github.yandex-team.ru/lp-constructor/constructor)). Они тоже обновляются через свой проект в [танкере](https://tanker.yandex-team.ru/project/lpc?branch=master).

Пометка: переводы в турбо – переводы для пользователей, переводы в lpc – переводы для контентов.

При добавлении нового компонента в танкер лучше убрать лишние языки, чтобы при синке не приехали финский, турецкий и тд. Убрать можно в [настройках кейсета](https://jing.yandex-team.ru/files/danigorokhov/uhura_2021-11-03T00%3A02%3A44.549382.jpg)

### Компоненты для создания контента ([LPC](https://github.yandex-team.ru/lp-constructor/constructor))

В Конструкторе Лендингов (LPC) существует [ручка](https://github.yandex-team.ru/lp-constructor/constructor/blob/b04fde5938bcb21becd0df78240421903bff37f1/api/src/controllers/turbo-json.ts#L245) для получения и [ряд специальных компонентов](https://github.yandex-team.ru/lp-constructor/constructor/search?q=path%3Alibrary%2Flc-sections+jobs) для управления контентом.

При работе с кодом Конструктора Лендиндов просьба ознакомиться с [рекомендациями от команды](https://github.yandex-team.ru/lp-constructor/constructor/blob/develop/CONTRIBUTING.md#рекомендации-к-написанию-кода).

### Тема форм для СВ

[Вики страничка со всей инфой](https://wiki.yandex-team.ru/users/danigorokhov/tema-form-dlja-sajjta-vakansijj/).

## Раскатка

### Граф

Раскатывается через влитие [новой версии графа в Аркадию](https://a.yandex-team.ru/arc_vcs/apphost/conf/verticals/JOBS) и [релиз через релизную машину](https://rm.z.yandex-team.ru/component/jobs_graphs).

### Jobs

Жмем кнопку `Run release`, перейдя по [ссылке](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fjobs&id=release)

> NB: Шаблоны раскатываются одновременно и на продакшн, и на хамстер окружения [рецептом в Няне](?RR).

### Turbo

Раскатывается несколько раз в неделю силами дежурных турбо и команды Jobs через кнопку в чатике. Связывайтесь с дежурными.

- [Релизный чатик Турбо](https://t.me/joinchat/-wpThHH9m6swZmQy) с кнопкой для раскатки
- [Хотфиксы в Турбо](https://wiki.yandex-team.ru/users/dakhetov/turbo/Kak-testirovat-turbo/Instrukcija-dezhurnomu-turbo/#ruchnoeotvedeniexotfiksaiegotestirovanie).

### LPC

Раскатывается командой Конструктора Лендингов несколько раз в неделю. Обращайтесь в поддержку команды LPC.

### Немного другой полезной информации про Apphost

- [Документация АппХоста](https://docs.yandex-team.ru/apphost/)
- [Чтиво об АппХосте](https://wiki.yandex-team.ru/users/koreil/apphost/)
- [Другая информация об АппХосте](./docs/pages/apphost)
- [Наш тестовый апстрим в хамстере](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hamster.yandex.ru/upstreams/list/upstream_shared_hamster_jobs_test/show/)

### Мониторинги сервиса

- [HQ панель в Няне с RR](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report-renderer-jobs/)
- [Дашборд 1](https://yasm.yandex-team.ru/panel/koreil._6Uh7Mg/) с сигналами ошибок шаблонов и фейлов графа в продакшне.

На фейлы источников с шаблонами настроены алерты в Telegram. Чтобы получать их, убедитесь, что вы [привязали свой логин](https://docs.yandex-team.ru/juggler/notifications/on_change#telegram).

В [Error Booster](https://error.yandex-team.ru/projects/apphost/projectDashboard?filter=service%20==%20JOBS%20AND%20additionalKeyValue%20in%20%22ctype%3A%20prod%22) удобно смотреть ошибки из общего интерфейса, а не по отедльным графикам, поскольку там отображаются подробности, например, версия графа и имя источника, породившего ошибку.

Пример запроса для продакшна: `service == JOBS AND additionalKeyValue in "ctype: prod"`
Пример запроса для hamster: `service == JOBS AND additionalKeyValue in "ctype: hamster"`