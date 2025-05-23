# external-skip

Плагин для [hermione](https://github.com/gemini-testing/hermione), отключающий во время запуска тесты из списка, указанного во внешнем файле.

## Установка

```bash
npm install @yandex-int/external-skip --save --registry https://npm.yandex-team.ru
```

## Использование

### Формат файла со списком отключаемых тестов

```
[
  { fullName, browserId, exclude, reason },
  ...
  { fullName, browserId, exclude, reason },
]
```

, где:

* `fullName` **[String]** – полное название теста (выступает в роли идентификатора теста);
* `browserId` **[String]** – идентификатор браузера, в котором тест будет отключен;
* `exclude` **[String[]]** – список номеров PR'ов в формате `pull/<number>`, для которых необходим принудительный запуск теста;
* `reason` **[String]** – текст, который будет указан в качестве причины отключения;

### Параметры

* `enabled` **[Boolean]** (необязательный, по умолчанию `true`) – отвечает за указание необходимости запуска плагина;
* `tool` **[String]** (необязательный, по умолчанию `hermione`) – отвечает за указание кастомного названия инструмента
* `isVCSAvailable` **[Boolean]** (необязательный, по умолчанию `true`) – указывает, доступна ли система контроля версий (`VCS` – `Version Control System`) в контексте выполнения плагина.

### Переменные окружения

* `ISSUE_KEYS` **[String]** (необязательный) – список идентификаторов задач со st.yandex-team.ru, разделённый запятыми.

## Логика работы плагина

При инициализации плагин считывает список отключенных тестов из внешнего файла и сразу после чтения тестов выполняет отключение тех тестов, которые по условиям являются отключенными (совпадение `fullName` и `browserId`). В случае, если задана переменная окружения `ISSUE_KEYS`, плагин будет проверять ее наличие в списке `exclude` и при необходимости не будет выполнять отключение тестов, в причинах отключения которых есть идентификаторы задач из списка значений `ISSUE_KEYS`.

### hermione

Подключить плагин в конфигурационном файле:

```js
module.exports = {
    plugins: {
        '@yandex-int/external-skip/hermione': {
            enabled: true,
            tool: 'hermione'
        }
    }
};
```
