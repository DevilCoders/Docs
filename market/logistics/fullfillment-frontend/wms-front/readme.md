# Клиент wms приложения

## Сборка в тимсити

[Проект в тимсити](https://teamcity.yandex-team.ru/project/Market_Delivery_Wms_Ui?mode=builds)

Некоторые неочевидные вещи:

- таски на деплой просто заводят тикет в кондукторе, но не дожидаются его выкатки (потому что на всё время ожидание это будет сжирать агента)
- деплой в престейбл разрешён только после выкатки в тестинг
- деплой в прод разрешён только после выкатки в престейбл
- интеграционные тесты по-умолчанию гоняются на престейбле, так что стоит выкатить туда пакет перед тестами
- в интерфейсе битбакета можно запустить интеграционные тесты - не надо так делать. К сожалению битбакет не умеет запрещать запуск тестов, но при этом требовать их прохождения.
- для гермионы нет репортера тимсити. отчёт по тестам надо смотреть в артефактах сборки

## Сборка в ЦУМЕ

[Проект в цуме](https://tsum.yandex-team.ru/pipe/projects/fulfillment/delivery-dashboard/wms-frontend)

Для деплоя на престейбл и продакт мы используем [ЦУМ](https://wiki.yandex-team.ru/market/development/infra/tsum) [созданный пайплайн](https://tsum.yandex-team.ru/pipe/projects/fulfillment/pipelines/wms-frontend) собирает приложение, запускает тесты, деплоит на престыйбл после чего запускаются e2e тесты, если все прошло успешно, можно задеплоить на продакт.

### Сборка приложения

Используем FrontSandboxBuildJob цум джобу, которая запускает MARKET_FRONT_BUILD_BASE сандбокс джобу.

* MARKET_FRONT_BUILD_BASE - билдит приложение и публикует дебиан пакет.
* FrontSandboxBuildJob - Создает Conductor ресурс, для деплоя его на сервера.

Для запуска тестов запускаем SimpleFrontSandboxBuildJob которая в свою очередь опять запускает FrontSandboxBuildJob

* SimpleFrontSandboxBuildJob - позволяет задать команду которую исполнит FrontSandboxBuildJob, но в отличие от FrontSandboxBuildJob эта джоба не сможет создать COnductor ресурс.

Далее запускается деплой на сервера с помощью кондуктор джобы



## Локальная разработка

```bash
# выбираем нужную версию ноды, можно не делать каждый раз
nvm use
# ставим необходимые пакеты, требуется выполнять, если изменился package.json
npm i

# для запуска в связке с бэкендом
API_HOST='http://dev-backend-host:123' npm start

# для запуска на моках
MOCK_CLIENT=1 npm start
# или
npm run mock

# для запуска на другом порту
PORT=8183 npm start
```
Открываем [тут](http://localhost:8080/ui/)

## Юнит-Тесты

```bash
nvm use
npm i
npm test
```

## Гермион-тесты

```bash
nvm use
npm i
```

Далее нужно в одном терминале запустить локальный селениум
```bash
nvm use
npm run selenium

# после первого запуска можно запускать немного быстрее:
npm run selenium:start
```

Для локальных тестов, в другом терминале запустить сам клиент
```bash
nvm use
API_HOST='http://dev-backend-host:123' npm start
```

И в другом терминале запустить сами тесты
```bash
nvm use
npm run test:hermione
```

Тесты можно запустить не только на локальном клиенте, но и стороннем хосте (тогда локально его запускать не нужно)
```bash
nvm use
BASE_URL='http://some-host-with-client.ru' npm run test:hermione
```

Плюс к тому можно использовать селениум-грид, тогда не нужно запускать локальный селениум (не работает для локального тестирования)
```bash
nvm use

GRID_URL='http://selenium:selenium@sg.yandex-team.ru:4444/wd/hub' BASE_URL='http://some-host-with-client.ru' npm run test:hermione
# - или если нужен именно этот грид, то
BASE_URL='http://some-host-with-client.ru' npm run test:hermione:grid
```

## Сборка

```bash
nvm use
npm i
npm run build
```

------
PS. можно не вызывать каждый раз `nvm use`, если установить дефолтную версию ноды:
```bash
nvm install 12
nvm alias default 12
```

## I18n
Для лучшего контроля текстовой информации используется связка [Tanker](https://doc.yandex-team.ru/Tanker/general-info/concepts/theory.html) и [@yandex-int/i18n](https://a.yandex-team.ru/arcadia/frontend/packages/i18n). Если коротко, то используется схема локализации [BEM.I18N](https://islands-lego.yandex-team.ru/doc/practics/localization/)

[Tanker](https://doc.yandex-team.ru/Tanker/general-info/concepts/theory.html) является хранилищем мапы `ключ: текст` и инструментом для синхронизации и нахождения ключей в коде с [проектом](https://tanker.yandex-team.ru/?project=WMS_FRONT).

Библиотека [@yandex-int/i18n](https://a.yandex-team.ru/arcadia/frontend/packages/i18n) позволяет считывать мапу и отображать текст в компонентах по ключу.

### Порядок работы

* Танкер использует OAuth-токен для авторизации к своему API. Для генерации персонального токена перейдите по [ссылке](https://nda.ya.ru/3SjQY7). Затем экспортируйте ключ в ваш $HOME/.profile (или .bash_profile и .zshrc, если не сработало), добавив
export TANKER_API_TOKEN="Тут ваш OAuth токен для Танкера"

* Если в компоненте необходимо отобразить текст:
    1. Ключ = текст на русском
    2. Не разбиваем логические фразы на несколько ключей.
    3. Не забываем про параметризацию и плюрализация, прочитать можно [тут](https://a.yandex-team.ru/arcadia/frontend/packages/i18n)
    4. Пример:
    ```js
    import { useI18N } from '@yandex-int/i18n/lib/react';
    import * as keyset from '@/project/project.i18n';

    export const Component = () => {
        const i18N = useI18N(keyset);
        return (
            <div>{i18N('Тут нужный текст = ключу')}</div>
        );
    };
    ```
    5. Если есть отображаемый текст вне реакт компонент, нужно использовтаь так:
    ```js
    import i18n from '@yandex-int/i18n';
    import * as keyset from '@/project/project.i18n';

    const i18N = i18n(keyset);

    export const someAction = declareAction('some action', (result, store) => {
        store.dispatch(
            AddNotification({
                theme: 'success',
                title: i18N('Успех'),
                text: i18N('Настройки СГ для партии успешно обновлены'),
            })
        );
    });
    ```
    6. Важно! Параметр функции `i18N()` - должен быть строчкой, не использовать переменные или [Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

    7. В проекте можно добавлять в админке танкера или через апи динамические кейсеты (словари) не привязанные жестко к ключами. Их можно использовать например для загрузки бэкендовских словарей. Для этого нужно в админке создать кейсет с :js на конце. Они при пулле ключей сохраняются в папке src/commonTankerGlossary. Они не предназначены для редактирования и создания ключей непосредственно в коде фронтенда

* После того как все нужные ключи добавленны в проект и согласованны нужно их загрузить в Танкер

    `npx tanker push` - пробежит по всему проекту, найдет все ключи, отберет новые ключи и попытается их загрузить в [проект танкера](https://tanker.yandex-team.ru/?project=WMS_FRONT). Для этого возможно потребуется дополнить информацию о ключах (кейсет, дефолтное значение и т.д). После этого новые ключи появятся в проекте танкера, но локальные мапы не обновлятся, для этого их нужно синхронизировать.

* Обновление значений ключей и добавление вновь появившихся

    `npx tanker pull --force` или `npx tanker pull -f` - добавит новые ключи и обновит необходимые, а так же разобъет их по проектам для того что бы их использовал @yandex-int/i18n в нужных компонентах

* **Не забудте закоммитить все изменения, включая папку `.tanker`**

### Полезные ссылки
* [Cхема локализации BEM.I18N](https://islands-lego.yandex-team.ru/doc/practics/localization/)
* [Проект танкера](https://tanker.yandex-team.ru/?project=WMS_FRONT)
* [Доки использования @yandex-int/i18n](https://a.yandex-team.ru/arcadia/frontend/packages/i18n) (мы используем подход с хуками)
* [Доки для использования Tanker CLI](https://a.yandex-team.ru/arcadia/frontend/packages/tanker-kit)

## Кодогенерация https://www.hygen.io/docs/templates/
`hygen apiMethod new --flow outbound --project consolidation --name test` - сгенерировать метод test в апи outbound/consolidation

`hygen project new --flow outbound --project consolidation --readableAppName Консолидация` - сгенерировать проект consolidation во флоу outbound

`hygen page new --flow outbound --project consolidation --name test` - сгенерировать inputPage страницу test в outbound/consolidation/pages

`hygen tablePage new --flow admin --project consolidation --name test` - сгенерировать страницу с таблицей test в outbound/consolidation/pages

В целях уменьшения привязки к изменчивому коду для разметки использовать комментарии вида `// GENERATOR: Example text`. Исключениями можно считать начало/конец файла и т.п.
