# WALL-E UI

Основан на макетах https://app.zeplin.io/project/5b0ebb409c589aa53eebd545

Используется технологический стек: React на TypeScript 3.1

Проект был забутстраплен, с помощью утилиты `create-react-app --typescript`


## Установка и сборка

Собственной системы сборки проект не имеет, используется `react-scripts` (для TypeScript)

Пока не понадобится что-нибудь ну очень экзотическое, экстрактить конфиг webpack я не планирую.

### Arc hooks

Для поддержки хуков необходимо создать файл `.arcconfig` рядом с директорией `arcadia` и вставить текст:
```
[pre-commit-hook "infra/walle/webapp"]
    pre-commit = infra/walle/webapp/.husky/pre-commit
[pre-push-hook]
    pre-push = infra/walle/webapp/.husky/pre-push
```

## Зависимости от библиотек Яндекса

[lego-on-react](https://lego.yandex-team.ru/libs/islands/) - react версия LEGO, мелкие контролы: кнопки, чекбоксы и т.п.
[@yandex-infracloud-ui/libs](https://khoden.infracloud.yandex-team.ru/_ui/) - библиотека отдела интерфейсов облачной инфраструктуры

## Внешние зависимости

* RxJS v6 - для организации потоков событий и прочей асинхронщины;
* numeral - для форматирования чисел;
* query-string - для кроссбраузерной работы с URL;
* lru-memoize - для мемоизации обработчиков событий в декораторе `@bindAndMemoize`;
* react-virtualized - для рендеринга больших списков;

(lodash, jquery и т.п. тащить в проект нельзя без предварительного обсуждения альтернативы)


## Верстка

Верстка идёт на чистом CSS по методологии [Reasonable System for CSS](http://rscss.io/index.html), адаптированной для react (CSS Modules).

Используется [CSS Grid Layout](https://caniuse.com/#feat=css-grid) и [CSS Flexible Box Layout Module](https://caniuse.com/#feat=flexbox).

Согласно сайту [caniuse.com](caniuse.com) они поддерживается в абсолютном большинстве браузеров.

## Архитектура проекта

| Папка                                             | Назначение                                                   |
| :------------------------------------------------ | :----------------------------------------------------------- |
| [/src/actions/](./src/actions/README.md)          | массовые действия над хостами и проектами                    |
| [/src/design/](./src/design/README.md)            | общие стили и иконки                                         |
| [/src/models/](./src/models/README.md)            | общие модели сущностей, модели API                           |
| [/src/rich_shared/](./src/rich_shared/README.md)  | большие переиспользуемые компоненты, специфичные для этого проекта |
| [/src/routes/](./src/routes/README.md)            | компоненты, которые рендерят роуты (страницы) и их подкомпоненты |
| [/src/services/](./src/services/README.md)        | общие классы с бизнес-логикой                                |
| [/src/shared/](./src/shared/README.md)            | библиотека компонентов                                       |
| [/src/state/](./src/state/README.md)              | Redux-state и редьюсеры                                      |
| [/src/stories/](./src/stories/README.md)          | общие stories для storybook (раздел other)                   |
| [/src/utils/](./src/utils/README.md) [deprecated] | мелкие утилиты, часто переиспользуются                       |

Более подробно можно прочитать в README.md внутри каждой папки.

### Управление стейтом

Как такового глобального стейта в приложении нет. Навигация управляется через History API, некоторые глобальные штуки легко реализуются через RxJS или реактовские контексты.

Пока что было принято решение не использовать redux и аналоги, т.к. не возникло необходимости. Если такая необходимость возникнет, следует её обговорить. На текущий момент профит от внедрения и поддержки считаю недостаточным.

Локальный же стейт легко покрывается встроенными в React возможностями. В частности новым Hooks API (в особенности хуком `useReducer`).

## CI

| Инструменты                                      | Назначение                                                         |
|:-------------------------------------------------|:-------------------------------------------------------------------|
| [Webhook](https://nda.ya.ru/3UWuyi)              | настройка веб-хуков в bitbucket (стандартные веб-хуки не работают!)|
| [gobabygo](https://nda.ya.ru/3UWuyx)             | внутренний CI-сервер, запускающий sandbox-таски                    |
| [sandbox](https://nda.ya.ru/3UWuz6)              | sanbox-таска                                                       |
| [nanny/dev](https://nda.ya.ru/3UWuz8)            | dev-контур                                                         |

## YC
Запуск в окружении ЯндексОблака требует наличия определенных доступов и секретов.
 - Доступ до Ticket Service (production) - https://puncher.yandex-team.ru/?id=612766bcb23337a4f9358920
 - Доступ до Session Service (production) - https://puncher.yandex-team.ru/?id=62060ef5e888da20bbf25c41
 - Секрет OAUTH_CLIENT_SECRET (production) - https://nda.ya.ru/t/X_qxCuFB4t5pwe
 - Секрет SA_PRIVATE_KEY (production) - https://nda.ya.ru/t/j4TfIwoO4t5pVo

 ### YC development
 - Локальная разработка возможна только в production-окружении
 - В production-окружении есть возможность работать только с 1 доменом - wall-e.cloud.yandex.ru, для локальной разработки необходимо добавить для него запись в /etc/hosts и заказть соответствующий сертификат
 - Веб-приложение запускается страндартным способом - npm run start
 - Для полноценной разработки необходимо запустить прокси: 
  - установить переменные окружения OAUTH_CLIENT_SECRET и SA_PRIVATE_KEY
  - в контроллере main.js раскомментировать фолбек на адрес веб-приложения
  - запустить прокси npm run start
 - Для работы c доменом по https придется запустить еще и nginx, конфиг можно взять из deploy/nginx-dev (в будущем попробуем удалить этот шаг в пользу запуска core)