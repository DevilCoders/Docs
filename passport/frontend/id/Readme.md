# Yandex.ID

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=passport-frontend/id-frontend&vcs=github)](https://oko.yandex-team.ru/github/passport-frontend/id-frontend)

Монорепозиторий личного кабинета ID.

## Сервисы
* [Новый личный кабинет](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/services/id)
* [История платежей](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/services/order-history) (deprecated)

## Пакеты
### Компоненты
* [design-system](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/design-system) — дизайн-токены темы (импортируются из [figma](https://www.figma.com/files/920787649869095992/project/1130419/MG-GUIDE))
* [id-components](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/id-components) — React-компоненты личного кабинета, см. [storybook](https://passport-static.s3.mds.yandex.net/story/@yandex-id/components/index.html?path=/story/button--default)
* [icons](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/icons) — пакет иконок, используемых на сервисах Яндекс.ID, можно посмотреть в storybook, запустив `npm run start:storybook` в `services/id`
* [id-suggest](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/id-suggest) — React-компоненты поиска по личным данным, см. [storybook](https://passport-static.s3.mds.yandex.net/story/@yandex-id/search-suggest/index.html?path=/story/suggest--default)

### Инфраструктурные пакеты
* [toolchain](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/toolchain) — инструменты для управления монорепозиторием (например, публикация затронутых пакетов)
* [ipreg](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/ipreg) — определяем внутреннюю сеть по IP
* [lint](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/lint) — общие конфиги линтеров
* [eslint-config](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/eslint-config) — пакет c конфигурацией ESLint
* [eslint-plugin-i18n](https://a.yandex-team.ru/arc/trunk/arcadia/passport/frontend/id/packages/eslint-plugin-i18n) — плагины ESLint для проверки переводов

## Документация
* [wiki](https://wiki.yandex-team.ru/id/dev)
* [Разработка](https://a.yandex-team.ru/arcadia/passport/frontend/id/docs/local-dev.md)
* [Настройка линтеров в редакторе](docs/editor-integration.md)
* См. также документацию в папках сервисов и пакетов
