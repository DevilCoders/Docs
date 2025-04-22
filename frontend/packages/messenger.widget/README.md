# Yandex.Messenger widget

Npm-пакет для подключения виджета Яндекс.Мессенджера

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.widget/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.widget)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.widget)<br>
[![dep health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.widget)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.widget)

## Содержание
- [Установка и интеграция](#установка)
- [Разработка](#запуск-стенда)

---

## Установка 
```
npm i @yandex-int/messenger.widget --registry=http://npm.yandex-team.ru
```

[Гайд по миграции со старого виджета](./doc/migration.md).

[Поваренная книга интеграций](./doc/cookbook.md) - Начни с нее.

[Решение проблем](./doc/troubleshooting.md) - Если при интеграции возникают проблемы.

[Интеграция](./doc/widget.md)

[Сборка своего бандла](../messenger.widget-cli/README.md)

[Storybook](https://messenger-test.s3.mds.yandex.net/storybook/widget/latest/index.html)

---

## Разработка

### Запуск стенда

Для запуска сторибука и туннелера используется команда `npm start`

Доступ к стендам будет по ссылке `https://{nickname}-2-ws2.tunneler-si.yandex.ru`

### Стенд в транке

Стенд доступен по ссылке `https://messenger-test.s3.mds.yandex.net/storybook/widget/{version}/index.html`

Где `version` нужная вам версия виджета

### Стили
#### css-переменные
CSS переменные, которые может переопределять хост должны быть явно объявлены в секции `:root`, каждая такая css переменная должна иметь описание (на их основе будет сформирована документация).

Сборщик стилей сам добавит префикс `--yandex-mssngr-widget` и смержит секции `:root` в одну.

### Перед пушем
Перед пушем необходимо запустить команду `npm run codegen`
Затем для сборки доки - перейти в папку `./scripts/codegen` и выполнить `node ./runner.js`

## Поддерживаемые браузеры
| <img src="docs/images/chrome.png" width="48" height="48" alt="Chrome logo"> | <img src="docs/images/firefox.png" width="48" height="48" alt="Firefox logo"> | <img src="docs/images/ie.png" width="48" height="48" alt="Internet Explorer logo"> | <img src="docs/images/opera.png" width="48" height="48" alt="Opera logo"> | <img src="docs/images/safari.png" width="48" height="48" alt="Safari logo"> |
|:---:|:---:|:---:|:---:|:---:|
| 47+ ✔ | 43+ ✔ | edge+ ✔ | 15+ ✔ | 9+ ✔ |