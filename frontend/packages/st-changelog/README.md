# st-changelog [![Build Status](https://drone.yandex-team.ru/api/badges/maxpon/st-changelog/status.svg?branch=master&style=flat)](https://drone.yandex-team.ru/maxpon/st-changelog)

Утилита для подготовки `debian/changelog` с использованием git-коммитов и компонентов и типов задач из Стартреке.

> Пример changelog с группировкой по компонентами и типами:
> ```
> yandex-weather-frontend (3.2.0) unstable; urgency=low
>
>   ## Touch-версия
>
>   [ Новое ]
>   * WEATHER-4099 Страница поиска (@maxpon)
>
>   [ Улучшения ]
>   * WEATHER-4066 Доработка шапки (@oggo)
>   * WEATHER-4054 Подровнять иконку ветра (@oggo)
>
>   [ Исправлено ]
>   * WEATHER-4093 Веб-приложение для Android имеет иконку iOS (@oggo)
>
>   [ Прочее ]
>   * WEATHER-4068 Ухудшающий эксперимент в таче (@oggo)
>
>   ## PDA-версия
>
>   [ Улучшения ]
>   * WEATHER-4072 Открутить jquery на pda версии (@pervikoff)
>
>   ## Desktop-версия
>
>   [ Исправлено ]
>   * WEATHER-3984 Не отображается "завтра" (@vaseker)
>
>   ## Общее
>
>   [ Улучшения ]
>   * WEATHER-4058 Оторвать плюс у положительной температуры для Турции (@maxpon)
>   * WEATHER-4033 Синхронизировать значение направления ветра в таче/десктопе (@pervikoff)
>   * WEATHER-3866 Актуализировать использование переводов (@pervikoff)
>   * WEATHER-3802 Обновить версию Лего (@oggo)
>
>   [ Прочее ]
>   * WEATHER-4092 Оторвать парамет ab_test (@maxpon)
>
>  -- teamcity <teamcity@yandex-team.ru>  Thu, 23 Apr 2015 16:22:56 +0300
> ```

> Пример changelog с группировкой только по типами задач:
> ```
> yandex-weather-frontend (3.2.0) unstable; urgency=low
>
>   ## Новое
>
>   * WEATHER-4099 Страница поиска (@maxpon)
>
>   ## Улучшения
>
>   * WEATHER-4066 Доработка шапки (@oggo)
>   * WEATHER-4054 Подровнять иконку ветра (@oggo)
>
>   ## Исправлено
>
>   * WEATHER-4093 Веб-приложение для Android имеет иконку iOS (@oggo)
>
>  -- teamcity <teamcity@yandex-team.ru>  Thu, 23 Apr 2015 16:22:56 +0300
> ```

## Установка

```bash
npm install -g st-changelog --registry=http://npm.yandex-team.ru
```

## Конфигурация

Положите файл конфигурации `.changelogrc` в корень проекта.

```json
{
  "queue": "<идентификатор очереди>",
  "token": "<токен доступа>"
}
```

Про токен доступа [написано](https://wiki.yandex-team.ru/tracker/api/#avtorizacija) в описании API. Токен также можно указать через опцию `--token`, переменные окружения `STARTREK_TOKEN` или `TOKEN`.

Опционально в файле конфигурации могут присутствовать настройки разделов changelog-файла:

 * `components {Object}` – компоненты очереди
 * `accordance {Object}` – соответствие разделов и типов задач
 * `names {Object}` – названия типов задач
 * `priority {Object}` – приоритет типов задач для сортировки (1 – высший, 99 – низший)

> ID компонентов можно получить так:
> `curl -s -H "Authorization: OAuth <token>" "http://st-api.yandex-team.ru/v2/queues/<queue_id>/components"`

Разделы changelog-файла:

 * new
 * improvement
 * fix
 * common
 * chore

Например:

```json
{
  "queue": "WEATHER",
  "token": "ABC…XYZ",
  "components": {
    "desktop": 16891,
    "touch": 14428
  },
  "accordance": {
    "improvement": ["improvement", "refactoring"],
    "fix": ["bug", "complaint"],
  },
  "names": {
    "new": "Огонь!",
    "chore": "Прочее всякое"
  },
  "priority": {
    "improvement": 1,
    "new": 2,
    "fix": 3,
    "chore": 4,
    "common": 5
  }
}
```

> По умолчанию
```js
ACCORDANCE = {
    new: ['newFeature'],
    improvement: ['improvement', 'refactoring'],
    fix: ['bug', 'complaint'],
    chore: ['task']
}
>
NAMES = {
    new: 'Новое',
    improvement: 'Улучшения',
    fix: 'Исправлено',
    common: 'Общее',
    chore: 'Прочее'
}
>
PRIORITY = {
    new: 1,
    improvement: 2,
    fix: 3,
    common: 98,
    chore: 99
}
```

## Использование

```bash
$ st-changelog [major | minor | patch | build NUMBER | version VERSION] <options>
```

Номер билда может быть задан также через переменную окружения `BUILD_NUMBER` или `CI_BUILD_NUMBER`.

**Опции**

```
--config <path> Использовать конфиг по указанному пути
--token         Использовать указанный Стартрек токен
--no-chore      Использовать в changelog только коммиты с упоминанием ID задачи в Стартреке
--no-editor     Не запускать редактор после подготовки changelog
--verbose       Выводить подробную информацию
--configs       Подготовить changelog для ./configs-package
--help          Показать справку
```
