# cypress-testcop-plugin

Плагин [cypress](https://www.cypress.io), отвечающий за `mute` тестов во время запуска.

## Установка

```bash
npm i @yandex-int/cypress-testcop-plugin --registry https://npm.yandex-team.ru
```

## Использование

```typescript
// plugins.ts
import { CypressTestcopPlugin } from '@yandex-int/cypress-testcop-plugin/build/plugin';

CypressTestcopPlugin({
    enabled: true,
    project: 'home',
    branch: 'dev',
    tool: 'cypress-e2e',
}, {
    reportFile: path.join(__dirname, '../../', 'cypress-report.json'),
    browser: 'touch-gramps',
})(on, config),
```

```typescript
// support.ts
import { CypressTestcopSupport } from '@yandex-int/cypress-testcop-plugin';

CypressTestcopSupport();
```

## Логика работы плагина

При инициализации плагин получает список отключенных тестов из [Тесткопа](http://testcop.si.yandex-team.ru) для указанного в конфиге проекта. При выполнении тесты пропускаются согласно списку, после чего формируется json отчет о пройденных, упавших и пропущенных тестах.

### Параметры плагина

* `enabled` **[Boolean]** (необязательный, по умолчанию `true`) – отвечает за указание необходимости запуска плагина;
* `tool` **[String]** (необязательный, по умолчанию `cypress`) - отвечает за указание инструмента/вида тестов, для которых запускается плагин;
* `project` **[String]** (обязательный) – название проекта, для которого включается плагин;
* `branch` **[String]** (обязательный) – название основной ветки репозитория, в котором находится проект; если проект находится и в гитхабе, и в аркадии одновременно, то нужно указывать основную ветку в гитхабе;
* `isVCSAvailable` **[Boolean]** (необязательный, по умолчанию `true`) – указывает, доступна ли система контроля версий (`VCS` – `Version Control System`) в контексте выполнения плагина.

### Параметры отчета

* `reportFile` **[String]** (необязательный) - путь создания файла json отчета. Отчет совместим с [Тесткопом](http://testcop.si.yandex-team.ru)

* `browser` **[String]** (необязательный) - имя браузера в json отчете. По умолчанию берется browserName из результатов прогона тестов

* `jsonEnabled` **[Boolean]** (необязательный, по умолчанию `true`) - сохранять ли json отчет

* `statsEnabled` **[Boolean]** (необязательный, по умолчанию `false`) - сохранять ли статистику в yt

* `ytProxy` **[String]** (Обязательный при `statsEnabled === true`) — прокси в yt, например, `hahn.yt.yandex-team.ru`

* `ytPath` **[String]** (необязательный) - путь до таблицы в yt, например, `//home/morda/mikstime/testcop`

### Переменные окружения

* `ISSUE_KEYS` **[String]** (необязательный) – список идентификаторов задач со st.yandex-team.ru, разделённый запятыми.

* `DISABLE_CYPRESS_TESTCOP` **[Boolean]** (необязательный) – отключение плагина

* `YT_OAUTH_TOKEN` **[String]** (необязательный) — токен авторизации для сбора статистики

## Road Map

✅ Поддержка Skipped тестов

✅ Формирование json отчета

✅ Поддержка Muted тестов

✅ Работа с переменной ISSUE_KEYS

❌ Сбор статистики
