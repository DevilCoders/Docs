# 🍟 Web-vendor:

### Локальная разработка

**Рекомендуется использовать Node версии v12.21.0**

#### Первый запуск

- Копируем dev-конфиг `cp config/default.yaml config/config.yml`
- Меням продовый стенд на свой (посмотреть доступные стенды - https://wiki.yandex-team.ru/eda/dev/stagings/)

```
vim config.yml
api:
  url: '%%stand%%'
```

- Устанавливаем зависимости и запускаем dev-server

```bash
npm install
npm run dev
# также можно указать стенд и другие параметры конфига через аргумент:
npm run dev -- --api.url https://erso-vendor.eda.tst.yandex.net
```

Если при первой установке npm install зависает на каком-то пакете и в консоли есть слова `Enter passphrase for key`, то необходимо отключить ввод passphrase при использовании ssh: https://wiki.yandex-team.ru/security/ssh/macos/#ispolzovanie

### Production сборка

```
npm i
npm run build
```

# Как открыть сборку PR

{branchName}.restapp-beta.tst.yandex.net

URL формируется из имени ветки, `/` заменяется на `-`.

Пример: имя ветки `feature/EDARESTAPP-1783-trendbox`, собранный пулреквест будет доступен по адресу `http://feature-edarestapp-1783-trendbox.restapp-beta.tst.yandex.net`

# Loki. Обновление скриншотов storybook

[Документация Loki](https://loki.js.org/command-line-arguments.html)

[Wiki](https://wiki.yandex-team.ru/eda/dev/web/vendor/loki.-skrinshotnye-testy-storybook/)

# Тесты

[Добавление тестовых селекторов](https://bb.yandex-team.ru/projects/EDA/repos/web_vendor/browse/tests/README.md#Селекторы)

Для тестирования используется [jest](https://jestjs.io/) и [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
Команды:

- `npm run test` для прогона всех тестов
- `npm run test:watch`  для запуска тестов в `watch` режиме

Все тесты кладутся рядом со стором/компонентом в папку **\_\_tests\_\_**.

### Тестирование MST моделей

Unit-тесты на бизнес логику моделей пишутся при помощи `jest` и мокалки [ApiMock](src/core-legacy/api/mock/ApiMock.ts).
Если необходимо замокать сценарий, где ответ одного запроса зависит от другого, есть вспомогательный класс [ApiScenario](src/core-legacy/api/mock/ApiScenario.ts).  
Сами моки создаются при помощи вспомогательной функции [createMockFactory](src/shared/test-utils/createMockFactory.ts).
[Пример](src/core-legacy/models/Orders/__tests__/Orders.test.ts)

### Тестирование React компонентов

Для правильного рендеринга со всеми необходимыми провайдерами используется функция [renderWithProviders](src/core-legacy/test-utils/index.tsx#88).
С её помощью инициализируется минимальный стейт приложения залогиненого пользователя.
Преимущественно тесты пишутся путем снятия снэпшотов верстки. Интерактивные элементы выбираются
либо по тексту, либо с помощью data-testid.
[Пример](src/core-legacy/common/pages/Communications/__tests__/Communications.test.tsx)

## Разработка нативных приложений на Android / Ios

- Устанавливаем cordova-cli v8 `npm install -g cordova@8.1.2`

#### IOS

Следуем инструции по установке Xcode | https://cordova.apache.org/docs/en/8.x/guide/platforms/ios/index.html#installing-the-requirements

Делаем подготовку приложения для ios

```
npm run cordova:prepare:dev -- --vendor ios
```

Далее открываем в xcode `cordova/platforms/ios` и запускаем приложение (кнопка `Play`).

#### Android

Следуем инструции по установке JDK / Android Studio / эмулятора https://cordova.apache.org/docs/en/8.x/guide/platforms/android/index.html#installing-the-requirements

Делаем подготовку приложения для android

```
npm run cordova:prepare:dev -- --vendor android
```

Далее открываем в Android Studio `cordova/platforms/android/` и запускаем приложение (кнопка `Play`) или запускам `cordova emulate android` в папке `/cordova`

### Разработка

Редактирование кода запуска нужно делать в папке `cordova/www`.
Весь код в папке `cordova/platforms` генерируется автоматически и не лежит в GIT.  
Запуск рабочей среды - через x-code (для первого запуска потребуется добавить аккаунт в команду разработки - https://stackoverflow.com/questions/39524148/requires-a-development-team-select-a-development-team-in-the-project-editor-cod)

Версии приложения и стейджинги для iOS приложения отличаются в зависимости от среды, для которой происходит сборка (`dev/test/production`).
Конфиги можно посмотреть в файле `config/default.yaml` в неймспейсе `cordova`.

### Релиз IOS

#### MDM - (adhoc версия) для партнеров

- Устанавливаем версию в `config/default.yaml`
- Делаем сборку в TeamCity > IosVendor > ios_adhoc
- Скачиваем `ipa`-файл
- Отправляем его письмом

с Релиз AppStore версии

- Устанавливаем версию в `config/default.yaml`
- Делаем сборку в TeamCity > IosVendor > ios_store
- Скачиваем `ipa`-файл
- Заливаем через Xcode / Application Loader (нужен apple id)

#### Релиз Android

- Устанавливаем docker-desktop https://www.docker.com/products/docker-desktop
- Запускаем `sudo bash cordova/ci/build.sh --stand %deploy_to% --mode %env.build_type%`

```bash
# Возможные аргументы: (аргументы не обязательны)
--stand picard (default - beta-vendor.eda.yandex)
--mode stand | beta | production | dev | adhoc (default dev)
# Пример:
sudo bash cordova/ci/build.sh --stand picard --mode dev
# Или релизная версия:
sudo bash cordova/ci/build.sh --mode production
```

- После сборки рабочая версия появится в корне проекта в директории `/apk`

### Как быстро посмотреть историю комитов между релизами

- Посмотреть все комиты между заданными с фильтрацией по сообщению

  ```sh
  arc log v5.17.0..HEAD --oneline | grep -E  '^[0-9a-f]{8} EDARESTAPP-'
  ```

- Посмотреть все тикеты между заданными комитами
  ```sh
  arc log v5.17.0..HEAD --oneline | grep -Eo  '^[0-9a-f]{8} EDARESTAPP-[0-9]+' | awk '{print($2)}' | sort | uniq
  ```

### Разработка нового нативного приложения

#### Дебаг страничка для тестирования нового натива

- Дебаг страничка доступна только на тестовом окружении в новом мобильном приложении,
  чтобы страничка была доступна поле show_debug_page в конфиге restapp_native должно быть true

#### Репозитории с нативным функционалом

- Android - https://bb.yandex-team.ru/projects/EDA/repos/android_vendor/browse
- IOS - https://bb.yandex-team.ru/projects/EDA/repos/ios_vendor/browse
