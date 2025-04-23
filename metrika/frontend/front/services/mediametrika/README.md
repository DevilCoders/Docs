# Yandex.Mediametrika

1) Заводим виртуалку по инструкции:

https://wiki.yandex-team.ru/JandexMetrika/frontend/dev_computer_for_everyone/

2) Ставим зависимости и запускаем:
```
cd ./frontend
npm run bootstrap -- --scope=mediametrika

cd ./services/mediametrika
make compose-up
```

## Вопросы безопасности

### Закрываем хэлсчеки от внешних пользователей

Из коробки стаб предлагает хелсчеки для отслеживания состояния необходимых смежных сервисов (например, доступность чёрного ящика, геобазы и базы данных). Пути, за которыми они скрыты, могут быть использованы для создания HTTP juggler-проверок в Qloud.

> :warning: Для того, чтобы эти пути не стали доступны внешним пользователям на публичном домене, необходимо в Qloud создать путь `/healthchecks/` и направить его в компоненту типа _http-balancer_, в параметре _Servers_ указав `http://any.yandex.ru/`.

### Mongo
У нас заведён [проект в mdb](https://yc.yandex-team.ru/folders/foo599vau2o7qoakss1n), где для монги заведено 2 кластера - для тестинга и продакшена.

В каждом кластере есть инструкция по подключению при нажатию на кнопку "Подключиться" в верхней части экрана.

Краткий пересказ для терминала:

1) Установить клиент [mongo](https://docs.mongodb.com/v4.0/tutorial/install-mongodb-on-os-x/) по инструкции;
2) Установить сертификат:

```bash
mkdir -p /usr/local/share/ca-certificates/Yandex && curl "https://crls.yandex.net/allCAs.pem" > /usr/local/share/ca-certificates/Yandex/YandexInternalRootCA.crt
```

3) Исполнить команду ниже. в параметр `--host` подставить хосты из интерфейса `mdb`:

```bash
mongo --norc --ssl --sslCAFile /usr/local/share/ca-certificates/Yandex/YandexInternalRootCA.crt --host '<PUT_HOST_HERE>' -u admetrica --ipv6 admetrica -p
```

4) Будет запрошен пароль от монги (НЕ пароль от твоего аккаунта). Его можно взять из [секретницы](https://yav.yandex-team.ru/secret/sec-01dc2481gxrcw93954063hg8ra/explore/versions);
5) Profit. Не сохраняй пароль в открытых источниках.

## Доступные команды

Команда | Действие
------------ | -------------
dev | Запуск tvmtool и приложения для локальной разработки
build:production | Запуск production сборки скриптов и стилей
lint | Проверка TypeScript и CSS кода на codestyle
i18n:pull | Выгружает переводы для текущей ветки

## Работа с переводами

### Работа с tanker

* Ссылка на проект в танкере https://tanker.yandex-team.ru/?project=adfox-adv
* Работа в tanker-е ведётся в отдельных ветках.
* В интерфейсе танкера создайте ветку с названием Вашей текущей ветки.
* Внесите необходимые изменения.
* Выгрузите изменения при помощи команды npm run i18n:pull.
* После мёрджа ветки в arcadia, смёрждите ветки в интерфейсе tanker-а.

> :pushpin: Добавить автоматический мёрдж веток после слияния

> *Nota bene* При необходимости можно выгрузить переводы для ветки, отличной от текущей ветки. Для этого используйте переменную окружения TANKER_BRANCH (например TANKER_BRANCH=master npm run i18n:pull)

### Работа с компонентом `<I18n />`

* Оберните компонент для которого требуется получить локализованную строку в компонент `<I18n />`.
* Передайте компоненту `<I18n keyset={keyset} />` кейсет для поиска ключей.
* В качестве потомка создайте функцию, аргументом которой будет являться функция i18n от данного кейсета.
* Функция i18n принимает 2 параметра: название ключа и опциональные параметры, среди которых может быть параметр count, который используется для получения множественных форм.

```tsx
    /*
     * Директория ./ExampleKeyset.i18n с содержимым формируется автоматически при выполнении npm run i18n:pull
     */
    import * as keyset from './ExampleKeyset.i18n';

    <I18n keyset={keyset}>
        {(i18n) => (
            <div>
                {i18n('test-key-with-params', {
                    paramName: 'testParam',
                    count: 10
                })}
            </div>
        )}
    </I18n>
```

* При необходимости, можно получить не локализованную строку, а исходный массив, содержащий части ключа и подставленный параметр. Для этого используйте компонент <I18nRaw />.

```tsx
    /*
     * Директория ./ExampleKeyset.i18n с содержимым формируется автоматически при выполнении npm run i18n:pull
     */
    import * as keyset from './ExampleKeyset.i18n';

    <I18nRaw keyset={keyset}>
        {(i18nRaw) => (
            <p>
                {i18nRaw('test-key-with-params', {
                    paramComponent: <Сomponent />
                })}
            </p>
        )}
    </I18nRaw>
```

## Документация

### Сборка релизов

#### Сборка нового релиза
1) Заходим в https://sandbox.yandex-team.ru/, жмём `Create task`. В поле выбора типа таска пишем `METRIKA_FRONTEND_RELEASE`
<details>
<summary>Скриншоты</summary>

![главная](https://jing.yandex-team.ru/files/rifler/Tasks__Sandbox_2019-04-16_21-43-27.png "главная")

![создание таска](https://jing.yandex-team.ru/files/rifler/Tasks__Sandbox_2019-04-16_21-46-57.png "создание таска")

</details>


2) Попадаем на страницу создания таска. В низу страницы находим раздел `Task custom parameters`. Его нужно заполнить:
- Поле `Сервис` - `mediametrika`;
- Чекбокс `Новый релиз` - выставлен;
- Поле `Версия предыдущего релиза` - необходимо ввести версию со страницы https://media.metrika.yandex.ru/version.

После чего жмём кнопку `Run`

<details>
<summary>Скриншоты</summary>

![параметры](https://jing.yandex-team.ru/files/rifler/Task_414574896_METRIKA_FRONTEND_RELEASE_2019-04-16_21-51-28.png "параметры")

</details>

3) Ждём его завершение. Таск должен:
- Создать релизную ветку в репозитории с именем `release-mediametrika-2.xxxxxx`, где `xxxxxx` это id таски в sandbox;
- Создать релизный тикет в стартреке, прилинковать к нему все нужные задачи;
- Собрать и раскатить сервис на тестинг https://test.media.metrika.yandex.ru. На странице /version должна отобразиться новая версия - `2.xxxxxx.1`

#### Обновление текущего релиза
Во время тестирования будут находиться баги.
1) Пулл-реквесты с исправлениями нужно делать в ветку `release-admetrica-2.xxxxxx`;
2) После сигнала от тестировщиков, что можно обновлять тестинг, необходимо повторить действия в sandbox, за исключением чекбокса `Новый релиз`. `Версия предыдущего релиза` нужно взять с тестинга вместо прода - https://test.media.metrika.yandex.ru/version


### Дебаг бандлов статики

Нужно запустить обычную сборку проекта с переменной окружения `WEBPACK_DEBUG_CHUNKS`, например:
```bash
WEBPACK_DEBUG_CHUNKS=1 npm run dev
```

После завершения сборки вот здесь http://127.0.0.1:8888 запустится [`webpack-bundle-analyzer`](https://github.com/webpack-contrib/webpack-bundle-analyzer) с графическим представлением содержимого получившихся бандлов.


### Дебаг Typescript

#### Получение текущей статистики проекта из компилятора TS

Запуск команды `npm run ts-stats` запустит компиляцию TS и выведет статистику по проекту в таком виде:
```
Files:          1694
Lines:        214040
Nodes:        761018
Identifiers:  261023
Symbols:      428843
Types:        203355
Memory used: 520808K
I/O read:      0.61s
I/O write:     0.00s
Parse time:    4.90s
Bind time:     1.69s
Check time:   14.07s
Emit time:     0.00s
Total time:   20.66s
```

Количество типов, указанное в `Types` не должно расти слишком быстро, по идее резкое увеличение числа типов свидетельствует о какой-нибудь проблеме в проекте или зависимостях.
Если увеличение типов было обнаружено не сразу, то можно пройтись по коммитам в истории обратно и посмотреть в результате каких изменений произошел резкий рост.

#### Когда имеет смысл обращать внимание на количество типов:

- При написании и широком использовании рекурсивных типов (Например, в `createReducer` из `typesafe-action`)
- При обновления зависимостей, в частности самого `typescript`

#### `createReducer`

В настоящий момент в проекте основной причиной роста количества типов
является `createReducer` из `typesafe-actions`.
Явное перечисление всех экшенов, используемых редюсером помогает снизить этот рост.

Например, при таком импорте всех экшенов:
```ts
import * as actons from 'client/store/actions/someFeature';
```

лучше вместо такого объявления
```ts
type Actions = ActionType<typeof actions>
```

писать список из только реально используемых в редюсере экшенов:
```ts
type Actions = ActionType<
    | typeof actions.doSmth
    | typeof actions.doAnotherThing
>;
```

Дальше по коду использование получившегося типа `Actions` будет выглядеть примерно вот так:
```ts
const reducer = createReducer<State, Actions>(initialValue)
    .handleAction(actions.doSmth, (state, action) => {

    }
```

- В случае, если в редюсере используются все импортируемые экшены, то явное их перечисление уже необязательно, т.к. не сэкономит ничего.
- Для асинхронных экшенов нет заметной разницы между указанием всего экшена
  `typeof actions.asyncAct` и только его части `typeof actons.asuncAct.success`,
  поэтому достаточно указания `typeof actions.asyncAct` без уточнения до request/success/failure.

`createReducer` собираются в 5 версии `typesafe-actions` переписать и упростить ([issue на github](https://github.com/piotrwitek/typesafe-actions/issues/143)),  так что возможно эта проблема пропадет или по крайней мере будет менее выражена.
Но в любом случае потребуется внимательно посмотреть на то, что произойдет с количеством типов после обновления на 5 версию.
