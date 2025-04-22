# Как добавить `/canary` в ваш репозиторий?

Для этого необходимо иметь 2 файла:
1. `.canary.json`, где будет собран необходимый конфиг для работы команды ([инструкция](#canary-config))
1. `golden.js`, где собран список сервисов, в которые будут открываться PR для проверки ([инструкция](#golden-config))

## <a name="canary"></a>Настройка для работы команды /canary

1. Добавьте в хуки репозитория
**Payload URL**:  https://hoolistener.common-int.yandex-team.ru/v1/comment

    Для того, чтобы обрабатывать комментарии, мы используем сервис [**Hoolistener**](https://github.yandex-team.ru/lego/islands/blob/dev/services/hoolistener/README.md)

<img width="982" alt="2019-08-26 15 58 09" src="https://media.github.yandex-team.ru/user/6503/files/c74e1980-c81a-11e9-8ad2-73331c8d60ce">

2. **Let me select individual events:** issue_comments
<img width="734" alt="2019-08-26 15 58 00" src="https://media.github.yandex-team.ru/user/6503/files/c6b58300-c81a-11e9-8fad-d38f5bbddea2">

3. Добавьте в owner всех нужных npm пакетов `lego-changelogger`
`npm owner <package> add lego-changelogger@yandex-team.ru`


4. Настройте `prepublishOnly` секцию в `package.json` пакетов, если перед публикацией необходимо произвести какие-то операции над пакетов: **например, скомпилировать typescript**.

5. **Пишите коммиты по [conventional commits](https://github.yandex-team.ru/lego/islands/tree/dev/contribs#соотношение-type-и-semver-версии-которая-будет-выпущена-в-npm)**

## <a name="canary-config"></a>Инструкция к .canary.json

[Пример конфигурации в репозитории Лего](https://github.yandex-team.ru/lego/islands/blob/dev/.canary.json)

Добавьте `.canary.json` в корень вашего репозитория и заполните его следующим образом.

* `trendboxOwner` — owner для создания Trendbox задачи.
* `goldenPath` — путь до golden-config.
* `install` — команда для установки зависимостей.

Пример
```
{
    "trendboxOwner" : "LEGO_TRENDBOX_CI",
    "goldenPath": "configs/golden.js",
    "install": "lerna exec npm ci"
}
```

## <a name="golden-config"></a>Инструкция к golden.js

[Пример конфигурации в репозитории Лего](https://github.yandex-team.ru/lego/islands/blob/dev/configs/golden.js)

Добавьте `golden.js` в ваш репозиторий и перечислите в нём все golden сервисы, заполнив их в следующей форме.

* `owner` — owner репозитория сервиса.
* `repo` — название репозитория сервиса.
* `forkOwner` — автор fork.
* `packagePaths` — пути до package.json файлов в репозитории сервиса.
* `baseBranch` — название основной ветки в репозитории сервиса.

Укажите `false &&` перед объектом, если хотите закомментировать данный сервис. Когда вам понадобится его убрать, достаточно будет убрать эту строку

Оберните всё содержимое в `module.exports` и передайте массивом

Пример итогового файла

```
module.exports = [
    {
        owner: 'lego-integrations',
        repo: 'lego-merch',
        forkOwner: 'lego-integrations',
        packagePaths: ['.', 'tshirts'],
        baseBranch: 'master'
    },
    false && { // этот сервис будет заскипан
        owner: 'direct',
        repo: 'dna',
        forkOwner: 'lego-integrations',
        packagePaths: ['.'],
        baseBranch: 'master'
    },
    {
        owner: 'search-interfaces',
        repo: 'frontend',
        forkOwner: 'lego-integrations',
        packagePaths: ['services/tutor', 'services/ydo', 'services/patents'],
        baseBranch: 'master'
    },
    ...
]
```
