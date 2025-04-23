# @yandex-int/release-to-infra

[![version](https://badger.yandex-team.ru/npm/@yandex-int/release-to-infra/version.svg)](https://npm.yandex-team.ru/-/ui/?text=@yandex-int/release-to-infra)<br>
[![dist health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/release-to-infra)](https://oko.yandex-team.ru/pkg/@yandex-int/release-to-infra)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/release-to-infra)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/release-to-infra)

Cli-утилита для отправки информации о релизе в infra.yandex-team.ru.

## Использование

```bash
release-to-infra --config .config/infra.js --appVersion 1.2.3 --env production
```

or

```bash
npx @yandex-int/release-to-infra --no-install --config .config/infra.js --appVersion 1.2.3 --env production
```

## Конфиг

Любой формат, который зареквайрит js.

Типизация конфига:
```typescript
interface SourceConfig {
    ticket: {
        // Поля не обязательны, возьмется те, которые есть.
        Queue?: string;
        Summary?: string;
        Tags?: string;
        // Не обязательный, по умолчанию tested, closed
        Status?: string | string[];
    },
    serviceId: number;
    environmentIds: Record<string, number>;
    templates: Record<string, {
        title: string;
        description: string;
    }>;
}
```

Пример конфига:

```javascript
module.exports = {
    ticket: {
        Queue: 'FOORELEASE',
        Summary: 'my_service/v{{version}}',
        Tags: 'release',
        Status: ['tested', 'readyForRC', 'RC'],
    },
    serviceId: 123,
    environmentIds: {
        development: 124,
        production: 125,
    },
    templates: {
        development: {
            title: 'Релиз дева (v{{ version }})',
            description: 'Успели: {{ description }}',
        },
        production: {
            title: 'Релиз v{{ version }}',
            description: '{{ description }}',
        },
    },
};
```

## Доступы

Для работы скрипта необохдимы токены, которые будут переданы через переменные окружения:

- **STARTREK_TOKEN** Токен для работы со st.yandex-team.ru
- **INFRA_TOKEN** Токен для работы с infra.yandex-team.ru

## Опции

### config

Путь до конфига.

По умолчанию `.config/infra`.

```bash
release-to-infra --config .config/infra.js
```

### appVersion

Версия релиза.

**Обязательно.**

```bash
release-to-infra --appVersion 1.0.0
```

### env

Окружение для деплоя, по умолчанию production

По умолчанию `production`.

```bash
release-to-infra --appVersion X.X.X --env development
```

### date

Дата и время релиза.

По умолчанию будет текущее время.

```bash
release-to-infra --appVersion X.X.X --date "2020-12-02 15:04:00+03:00"
```

### endDate

Дата и время окончания релиза.

По умолчанию возьмется время из поля `date`.

```bash
release-to-infra --appVersion X.X.X --endDate "2020-12-02 15:04:00+03:00"
```

### noEmail

Не отправлять рассылку о релизе.

По умолчанию `false`.
Т.е. информация о релизе отправится по почте всем, кто на нее подписан.

```bash
release-to-infra --appVersion X.X.X --noEmail
```

### dryRun

Только попробовать, посмотреть что будет :)

По умолчанию `false`.
Используется, что бы проверить, что будет отправлено в infra.yandex-team.ru.

```bash
release-to-infra --appVersion X.X.X --dryRun
```
