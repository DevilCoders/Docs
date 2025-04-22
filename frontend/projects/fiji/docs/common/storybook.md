

# Storybook

## Автоматическая сборка для каждого PR и Dev

**Окружение**

Сторибук хранится на тестовом s3 и после билда(PR или DEV) происходит заливка новой версии
> Storybook обновится только если была запущена таска сборки

**Время жизни**
7 дней с момента заливки

***Пример ссылок***

`https://fiji-storybook.s3.mdst.yandex.net/story/fiji/index.html` - dev

`https://fiji-storybook.s3.mdst.yandex.net/story/fiji/pull-<номер PR>/index.html` - PR

**Как происходит деплой**
Процесс настройки бакета и работы с ним описан на [wiki](https://wiki.yandex-team.ru/search-interfaces/multimedia/images/storybook/)

## Локальная разработка

**Сборка и запуск**

`npm run strorybook` - запускает сборку и старт локального storybook. Сторибук будет доступен по адресу `http://localhost:6006/`
> Перед сборкой сторибука необходимо выполнить сборку проекта
> Сторибук собирается для того сервиса для которого была выполнена сборка проекта

**Локальный запуск с HTTPS**

По умолчанию сторибук локально запускается в http. Запуск в HTTPS возможен, но для этого нужен сертификат.
Параметры для запуска в официальной доке сторибука https://storybook.js.org/docs/react/api/cli-options#start-storybook

Пример запуска с сертификатом темплара, который лежит в `~/.config/templar/ssl/`, браузер будет ругаться, но запустит.
`npm run storybook -- --https --ssl-cert ~/.config/templar/ssl/rootCA.crt --ssl-key ~/.config/templar/ssl/rootCA.key`


## Как писать

Файл примера должен называться так: `Component@platform.stories.tsx`
Например: `Viewer@desktop.stories.tsx`

Пример должен называться так: `service/component/@platform`
Например: `video/components/Viewer/@desktop`

Для правильной установки всех необходимых классов на root необходимо использовать конфиги для scope.
Конфиги можно получить через утилиту `getFijiScope` указав имя необходимого конфига.
Конфиги `sakhalin`, `video`, `images` отвечают за правильную сборку css.
Например `getFijiScope('video')`
Описание конфига [.storybook/webpack.config.js](../../.storybook/webpack.config.js)

## Особенность сборки CSS

В конфиге postcss есть специальный плагин, который все каскады заворачивает в scope контейнер.
Это необходимо для правильной работы сторибука.
Но при разработке, может возникнуть ситуация что если компонент отрендерится вне scope контейнера, то от него отвалятся все css стили.
Например это возникает с компонентами на базе `Popup2`, когда сам попап рендерится в конце дом дерева.
![](https://jing.yandex-team.ru/files/ekurtaliev/2021-05-12_12.17.29-5kmag.png)

В таком случае, рекомендуется компоненту задать scope.

## Best practice

Смотри [docs/best-practices-react.md#паттерны-разработки](../docs/best-practices-react.md#паттерны-разработки)


## 🙅 Hermione

Тесты на Storybook не должны использовать сеть. Примеры должны работать локально.

