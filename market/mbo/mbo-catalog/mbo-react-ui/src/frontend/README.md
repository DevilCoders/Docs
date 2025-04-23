# React фронтенд в MBO

Сборка: `scripts/dev/run-mbo-react-ui.sh`

## Обновление зависимостей для ya make
для перегенерации зависимостей npm надо запустить скрипит update-arcadia-resources.sh из директории market/mbo/mbo-catalog/mbo-react-ui, после перегенерации в файл market/mbo/mbo-catalog/mbo-react-ui/src/frontend-node-and-modules/node-and-modules-in-jar/node_modules.ya.make будет залит новый идентификатор ресурса, после необходимо будет залить изменения в транк. 

## Запуск на aida
Для запуска необходимо запустить скрипт scripts/dev/run-mbo-react-ui.py

## Особенности сборки ya make
К сожалению нативная поддержка только начинает добавляться и находится на уровне беты.
В будущем node модули должны быть перенесены в модули типа TS_LIBRARY, пока так называется новый макрос, возможно название изменится.
Так как нет нативной поддержки, для сборки используется самописный костыль: market/mbo/arcadia_node/npm-run, костыль позволяет запускать npm средствами java, компилировать и запускать тесты.
К сожалению модуль EXECTEST не поддерживает RUN_JAVA_PROGRAM, а только RUN, поэтому результаты тестов определяются по успешности сборки.

## Особенности пайпов, кубиков и SB
Для запуска в sandbox обязательно добавление требование клиентского тега в кубике настройки: LINUX_FOCAL.
Без добавления этого тега ya package и ya make будут падать в SB, так как не смогут найти GLIBCXX, который необходим для запуска npm.

## Запуск в IDEA (без gradle)

### Простой вариант
1. Сделать конфигурацию на запуск MboUiMain (можно через Ctrl+Shift+F10)
2. Может ругнуться: если рабочая папка запуска не корень mbo - поставьте.
3. Может ругнуться: если нет tnsnames.ora - даст команду, как его принести куда надо.
4. Надо настроить ETCD и т.п., см. ниже

### СТАРОЕ
1. Сделать конфигурацию на запуск MboUiMain (можно через Ctrl+Shift+F10)
2. Прописать параметры VM: `-Dconfigs.path=mbo-react-ui/src/main/properties.d -Dlog4j.configurationFile=mbo-react-ui/src/main/conf/local/log4j2-test.xml -Djava.net.preferIPv6Stack=true -Djava.net.preferIPv6Addresses=true -Xverify:none -Denvironment=local`
3. BlackBox банит ноутбуки, варианты решения:
   - добавить -Dspring.profiles.active=no-auth в параметры VM, это полностью выключит авторизацию
   - добавить -Dspring.profiles.active=local-start в параметры VM, эта конфигурация использует небезопасную куку
4. Добавить ETCD_USERNAME и ETCD_PASSWORD в bash_profile, значения переменных можно найти здесь https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit
5. Добавить параметр VM -Doracle.net.tns_admin=<path-to-folder-with-tnsnames.ora>
   ```
   предварительно скачать файл и положить в локальную папку `scp aida.market.yandex.net:/etc/oracle/tnsnames.ora .`
   ! путь лучше указать относительный или абсолютный - ТИЛЬДА не раскрывается!! `-Doracle.net.tns_admin=./mbo-react-ui`
   ```
6. Проверить - http://localhost:8040/ui
7. PROFIT!

Плюсы: работает локально (логи/дебаг в одном окошке и сразу), запускается ощутимо быстрее, чем через гредл.
Минусы: нет авто-сборки фронта (она и не нужна для разработки, см. ниже), нет гредла - и соответственно какой-то его магии, что-нибудь может не заработать (но вроде всё ровно).

## Запуск UI

ВАЖНО! В webpack-react-и-компании есть отличный dev-режим, не надо разрабатывать методом полной сборки и перезапуска, это крайне неэффективно.

При первом запуске приложения нужно:

1. Скопировать файл с переменными окружения `cp .env.local.sample .env.local`

Для проксирования запросов можно использовать следующие хосты:

- http://mbo-react-ui.tst.vs.market.yandex.net - тестинг
- http://mbo-react-ui.tst.vs.market.yandex.net - прод
- https://mbo--mbo01mt.demofslb.market.yandex.ru - мультитестинг (где mbo--mbo01mt - id-шник среды тестинга)

2. В файл `/etc/hosts` (`C:\Windows\System32\Drivers\etc\hosts` - для Windows) добавить следующие записи:

```
127.0.0.1   localhost.msup.yandex-team.ru
127.0.0.1   localhost.msup.yandex.ru
```

3. "Нарезать" сертификат и приватный ключ и положить их в директорию ssl.local:

```bash
mkdir ssl.local
sed -n '/-----BEGIN PRIVATE KEY-----/,/-----END PRIVATE KEY-----/p' node_modules/@yandex-int/magicdev/data/yandex-team.pem > ssl.local/yandex-team.key
sed '/-----BEGIN PRIVATE KEY-----/,/-----END PRIVATE KEY-----/d;/^\s*$/d' node_modules/@yandex-int/magicdev/data/yandex-team.pem > ssl.local/yandex-team.crt
touch .env.local
echo 'SSL_CRT_FILE="ssl.local/yandex-team.crt"' >> .env.local
echo 'SSL_KEY_FILE="ssl.local/yandex-team.key"' >> .env.local
```

Варианты запуска дев-режима:

1. `gradlew :mbo-react-ui:npm_run_start` - самый простой, должен всё сделать, можно настроить билд-конфигурацию. Из минусов - чёрно-белый вывод консоли, плохо убивается (надо гасить nodejs через killall node).
2. Настроить nodejs 10+ на машинке, и использовать:

   ```bash
   cd mbo-react-ui/src/frontend
   npm install # 1 раз или когда поменялись либы
   npm start
   ```

Откройте страницу приложения [https://localhost.msup.yandex-team.ru:3443/](https://localhost.msup.yandex-team.ru:3443/).

При редактировании кода страница будет перезагружаться.

Статическая проверка синтаксиса (eslint) будет выводить ошибки в консоль.

Поставьте также расширения для браузера:

- [React Dev Tools](https://github.com/facebook/react-devtools#installation)
- [Redux Dev Tools](http://extension.remotedev.io/#installation)

## Запуск тестов UI

1. Также, как и дев-режим, но `npm_run_test` или `npm run test`, соответственно.
2. Запуск тестов работает из IDEA! Ctrl+Shift+F10 и всё.

## Сборка артефактов

`npm run build`

## definitions.ts - мостик между SpringMVC и TypeScript

Файлик `mbo-react-ui/src/frontend/src/java/definitions.ts` содержит сгенерированные стабы для контроллеров и для типов из них.

Обновляется через `./gradlew :mbo-react-ui:generateTypeScript` или через `npm run generate:definitions`

# Кодогенерация

Все новые страницы, компоненты и виджеты нужно создавать через эти генераторы, для повышения консистентности кода.

Создать новый компонент:

```bash
npm run generate:component
```

Создать новый виджет:

```bash
npm run generate:widget
```

Создать новую страницу:

```bash
npm run generate:page
```

После создания модулей страницы нужно прописать их в роутере.

# Темизация

В проекте используется themekit для:

- точечной темизации компонентов
- расширения существующих тем Лего

Бонусом получаем:

- возможность описывать токены в формате понятном для всех
- иерархическую структуру
- генерацию в любой формат (css/js/json/figma)

Themekit основан на [Style Dictionary](https://amzn.github.io/style-dictionary/) от Amazon.

Основная работа происходит с дизайн-токенами. Токены похожи на селекторы и CSS-свойства, например:

```yml
button:
  border:
    radius:
      value: '{units.border.radius.200.value}'
  size:
    s:
      fontSize: 13px
```

В значениях токенов можно использовать алиасы, они ссылаются на значения других токенов:

```yml
value: '{units.border.radius.200.value}'
```

Поддерживается сокращенный формат токенов:

```yml
button-size-s-fontSize:
  value: 13px
```

Для генерации CSS используем команду:

```bash
npm run build:themekit
```

Сгенерится файл со стилями, который содержит значения из Лего и значения из токенов. Сгенерированный файл со стилями импортируется в проект.
В будущем будет webpack-плагин, который будет собирать токены в buildtime.

Сгенерированные значения доступны как CSS-переменные.
Для примера выше это будут `--button-border-radius` и `--button-size-s-font-size`.

Просмотреть существующие токены в Лего можно на странице: https://lego.yandex-team.ru/themes-constructor

Основная тема приложения лежит в ```src/themes/default```, список токенов в виде css доступен в подпапке ```generated```

# Режим "в разработке"

Для новых фич, которые пока не хочется выкатывать на широкую аудиторию, но по которым хочется собрать некоторый фидбек, можно включать режим "в разработке".
Для этого нужно добавить к контейнерам класс dev-mode-only. Такие элементы будут показаны только пользователям, у которых установлена кука dev-mode.

Управлять режимом можно из консоли:
```javascript
document.cookie = 'dev-mode=y'; // включили dev-mode
document.cookie = 'dev-mode=';  // выключили dev-mode
```

# Status

Что хочется получить, и что есть, чего нет (раздел убираем, когда всё сделаем):

- ~~компонент с SpringMVC~~ - mbo-react-ui, отдельный, т.к. подселение SpringMVC 4.3 воткнулось в зависимости mbo-gwt (validator-1.0, когда спрингу нужен второй)
  - ~~TODO: в текущей конфигурации не читаются @Value внутри контроллеров - надо пофиксить (забавно, что на дев-сервере читаются) не хватало MboPropertiesConfig в нужнем месте~~
- ~~dev-по-кнопке/локальный запуск~~ - локальный запуск вообще норм
- ~~сделать деплой для этого компонента в RTC (вероятно, не стоит делать на железные машинки):~~
  ~~- сделать компонент по кнопке, чтобы всё зарегать~~
  ~~- настроить tsum-пайплайн~~
  ~~- сделать балансер для него~~
- ~~сделать развёртывание в МТ (насколько сложно там поднять ещё один докер?)~~
- ~~настроить nginx, чтобы проксировал запросы /ui на него~~
- ~~доделать базовые вещи по бэку:~~
  - ~~проверка прав (см. @SecuredRoles в mbo-category и авторизацию в GWT)~~
  - ~~проброс прав на клиент/отображение ошибки там~~
- настроить фронтенд и сборку:
  - ~~само приложение create-react-app, typescript, tslint~~
  - ~~сборку вместе с приложением~~
  - ~~генерацию definitions.ts~~
  - абсолютные импорты - пока что, судя по всему, [не судьба](https://github.com/facebook/create-react-app/issues/5585)
  - ~~тестирование: jest, enzyme - проверить, что всё норм и валит общую сборку, случись чего~~
- сделать базовый фронтенд:
  - ~~подключить конфиги с бэка~~
  - ~~завести Redux~~ - пока очень условно, нужно проработать эту тему
  - ~~завести роутинг~~ (асинхронный? - для начала можно не асинхронный - это сравнительно дёшево делается потом)
  - общий вывод ошибок (на основе того, что в `mbo-components`) - пока нет - алертами
- простой пример страницы:
  - ~~просто что-нибудь выводим с Counter компонентом~~
  - желательно что-нибудь тягаем с сервера - как пример работы/обработки ошибок
  - ~~пример теста (чтобы сразу можно было писать по образу и подобию)~~
  - пример теста с моком API
  - пример redux/epic-ов и компании?
- отдельная история - интеграция в GWT:
  - продумать протокол (примерно так - есть некоторый `getComponent(id: string) -> Promise<{mount(domElement), unmount(), call(props: any): any}>`
  - реализовать режим работы в фронте (скорее всего - просто по наличию значения в window вместо старта приложения мапим фабрику)
  - реализовать компонент GWT
- TODO по выносу общих частей:
  - fetch-api - нужно вытащить в отдельный пакет, для публикации springmvc-ts-generator
  - `commonErrorHandlers.ts`
