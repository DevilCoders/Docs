Яндекс.Избранное
=========================
[![OKO health](https://badger.yandex-team.ru/oko/repo/mm-interfaces/fiji/health.svg)](https://oko.yandex-team.ru/repo/mm-interfaces/fiji?statusFilter=all&repoFilter=collections)
### Содержание:

 - [Стэк технологий](#StackTechnology)
 - [С чего начать](#Begining)
 - [Разработка](#Development)
 - [Пул-реквесты](#RulesOfPullRequests)
 - [Структура копонента](#ComponentStructure)
 - [Переводы](#Translates)
 - [Счетчики](#Counters)
 - [Инлайн svg](#Svg)
 - [Серверная отладка](#ServerDebugging)
 - [Сборка плагинов](#BuildPlugins)
 - [Тестирование](#Testing)
 - [Эксперименты](#Experiments)
 - [Создание и выкатка релиза](#ReleaseCheckList)

### <a name="StackTechnology"></a>Дополнительные технологии, используемые в проекте:

 * [DI](https://github.com/ftdebugger/di.js/)
 Резолвер зависимостей. Применяется в основном для тестов для подмены данных

Тесты:

 * [Chai](http://chaijs.com/)
 * [Sinon](http://sinonjs.org/)

### <a name="Docs"></a>Сторонняя документация

 * [Backend docs](https://pdb-backend-test.n.yandex-team.ru/docs)
 Для просмотра используйте [плагин](https://chrome.google.com/webstore/detail/swagger-ui-console/ljlmonadebogfjabhkppkoohjkjclfai)
 * [Документация по тестированию](https://wiki.yandex-team.ru/collections/test)
 * [Размеры картинок в аватарнице](https://wiki.yandex-team.ru/collections/Avatarnica/)

### Дополнительно
 * При разработке можно использовать [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
 * Для поиска нужного компонента можно использовать [Storybook](http://pdb-storybook.n.yandex-team.ru),
который также доступен локально [по ссылке](https://localhost.yandex.ru:9003)


<a name="Begining"></a>С чего начать
====================

### <a name="Environment"></a>Подготовка окружения

Используемые версии:

* node - 12.18.1
* npm - 6.14.5
* gulp - 4.0.0

Установка:

    nvm install 12.18.1
    npm install -g npm@6.14.5
    npm config set registry https://npm.yandex-team.ru/

Установка etc hosts:

    127.0.0.1       localhost.yandex.ru
    127.0.0.1       localhost.yandex-team.ru
    127.0.0.1       local.yandex.ru

    127.0.0.1       local.yandex.by

Клонирование и установка зависимостей
Репозиторий коллекций находится в монорепе фронтенда по адресу https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections
Как работать с арк написано тут https://wiki.yandex-team.ru/search-interfaces/arc/
    - cd MY_PATH/collections
    - npm ci

Запросить доступы до секретов у команды фронтенда Избранного (https://abc.yandex-team.ru/services/collections-nodejs/):

- collections_nodejs_certs_dev: https://yav.yandex-team.ru/secret/sec-01dbfdh2kn4f6zvxq3pkje4j21/
- collections_nodejs_test: https://yav.yandex-team.ru/secret/sec-01db0n2m57eey1ds46dxckmfqf/

<a name="Development"></a>Разработка
==========

    gulp

После это будут подняты локальные серверы:
 * для веба `https://localhost.yandex.ru:9000/collections`
 * для админки `https://localhost.yandex-team.ru:9001`
 * для Hermione компонентов `https://localhost.yandex.ru:9002/`
 * сторибук `https://localhost.yandex.ru:9003`

Запуск с внешним доступом для отображения баннеров или чтобы показать коллеге. Обычно достаточно первого варианта

    gulp --public

Будет создан веб сервер на `https://your-name-123456-ci1.si.yandex.ru`

Прокси сервер для оффлайн страницы

    node utils/offline-proxy/index.js
    BACKEND_PROXY_API="https://localhost.yandex.ru:8051" gulp web

Открыть в браузере `https://localhost.yandex.ru:8051/offline/set/1`, чтобы включить, `https://localhost.yandex.ru:8051/offline/set/0` — выключить оффлайн.


### Когда задача готова к ревью
В задаче описать, какие компоненты были затронуты и что дополнительно могло быть затронуто, чтобы тестирование обратило на это внимание.

Необходимо запросить повторное ревью, если:
 1. Тестирование выявило баги и код был изменен;
 2. После исправления замечаний ревьювера;
 3. Если после ревью был изменен значительный кусок кода / обновилась логика.

### Если вас назначили ревьювером
SLA для просмотра Pull-Request 1 сутки.

<a name="RulesOfPullRequests"></a>Пул реквесты
==============================

### Правила создания пул реквестов

Все пул реквесты для коллекций должны быть созданы из ветки, которая именуется по следующим правилам:
`some-description.PODB-0000`

Если тикета нет, то указываем `TRIVIAL` вместо `PODB-0000`.

Commit message должен быть написан на русском языке.

Формат commit message следующий:

Если есть задача - `feat(collections): карточка фильмы`
Без задачи - `TRIVIAL: документация по танкеру`. Любой код, который влияет на пользователя, должен быть привязан к задаче


### <a name="PRIssues"></a>Диагностика проблем с пулл-реквестными стендами

0. Если вы не нашли проблему сами, а стенд все еще не поднимается, то сразу пишите дежурному по фронту. По горячим следам проще понять, что пошло не так. Текущего дежурного можно посмотреть [здесь](https://abc.yandex-team.ru/services/collections-nodejs/duty/).
1. Убедитесь что существует чек `Deploy`, и что связанная с ним sandbox задача успешно завершилась. Зайдите в лог и проверьте, что нет ошибок.
   Если чека нет, то проверьте правильность именования ветки. Правила описаны в пункте [Правила создания пул реквестов](#RulesOfPullRequests).
2. Проверьте, правильно ли была произведена сборка. Если были ошибки при сборке, то обычно их можно увидеть в лог файле `release.out.txt`,
   который можно найти в сэндбокс задаче. Обычно бот пытается собрать задачу 3 раза, прежде чем признать ошибку.
   Если за 3 попытки так и не удалось завершить успешно сборку, то бета поднята не будет. Ребейз или коммит заставит бота начать все с начала.
3. Найдите свою бету в няне. Это можно сделать со страницы [https://nanny.yandex-team.ru/ui/#/services/](https://nanny.yandex-team.ru/ui/#/services/)
   по номеру пул реквеста. Сервис называется по шаблону `pdb_nodejs_test_pr{number}`. Для стенда 9000 должен получится адрес
   `https://nanny.yandex-team.ru/ui/#/services/catalog/pdb_nodejs_test_pr9000/`. Если беты нет, а чеки есть - переходите к пункту 0.
4. Бета должна быть в статусе `Active`, если это не так, то нужно смотреть почему она не поднялась.
   На обновление беты обычно уходит пара минут, если процесс затягивается, скорее всего бета не может подняться. Чаще всего это связано с ошибкой в коде или при сборке
   из-за которой стенд не может подняться. Логи можно найти в файлах `pdb_node.err` и `pdb_node.out`. Получить их содержимое можно
   напрямую из контейнера [https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#shell-into-container](https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#shell-into-container)
   или по кнопке ISS. Если нет прав - переходите к пункту 0.


<a name="ComponentStructure"></a>Структура компонента
==========
Для создания новых компонентов можно использовать команду ```npm run new-component```

* Папка с копонентом должна иметь следующую структуру:
```
.
├── ComponentName.tsx           Сам копонент
├── ComponentName.scss          Базовые стили
├── ComponentName.gemini.tsx    Gemini-тест
├── ComponentName.i18n.json     переводы
│
├── ComponentName@desktop.scss  дескопные стили(опционально)
├── ComponentName@mobile.scss   мобильные мобильные(опционально)
│
└── ComponentName.gemini.scss   стили необходимые для тестирования скриншотами(опционально)
```
* Название блока в стилях компонента должно начинаться с префикса `cl-`

```typescript jsx
import * as React from 'react';

import { classHash } from 'helpers/class-hash';

import 'components/ComponentName/ComponentName.scss';

if (IS_DESKTOP) {
    require('components/ComponentName/ComponentName@desktop.scss');
} else {
    require('components/ComponentName/ComponentName@mobile.scss');
}

export interface ComponentNameProps {
    className?: string;
}

export function ComponentName(props: ComponentNameProps) {
    let { className } = props;

    return (
        <div
            className={classHash('cl-component-name', {}, className)}
        >
            code here
        </div>
    );
}

```
* Расширяющий компонент также может иметь свои стили и передавать их базовому компоненту
```typescript jsx
import * as React from 'react';

export function ExtendedComponentName() {
    return (
        <ComponentName className="cl-extended-component-name">
            <Button className="cl-extended-component-name__button" />
        </ComponentName>
    );
}
```


<a name="Translates"></a>Переводы
====================

Проект в [танкере](https://tanker.yandex-team.ru/project/pdb)

1. Создаем рядом с компонентом файл с именем компонента и расширением .i18n.json (Например для UserAvatar.tsx будет UserAvatar.i18n.json)
2. Содержимое представляет собой примерно следующий формат:

```json
{
    "simple": {
        "context": "Пример простого перевода",
        "translations": {
            "ru": "Купить"
        }
    },
    "withVars": {
        "context": "Пример перевода с переменными",
        "translations": {
            "ru": "Купить за __price__"
        }
    },
    "withHtml": {
        "context": "Пример перевода с HTML",
        "translations": {
            "ru": "Купить за __price__ <span class=\"rur\">руб.</span>"
        }
    },
    "withPlural": {
        "context": "Пример плюральных форм",
        "translations": {
            "ru": [
                "Закроется через __count__ секунду",
                "Закроется через __count__ секунды",
                "Закроется через __count__ секунд"
            ]
        }
    }
}
```

3. В переводы можно вставлять переменные через `__varName__` синтаксис.
Если в переводе есть специальная переменная count, то перевод начинает поддерживать плюральные формы.
Для русского языка плюральные формы идут в порядке 1, 2, 5, 0
4. Переводы кроме русского можно не заполнять
5. Использование перевода примерно такое:

```js
import * as translates from './UserAvatar.i18n.json';

export function Example() {
	return (
		<div>
			Просто перевод: {translates.simple()}

			Переменные: {translates.withVars({ price: 1000 })}

			HTML: {translates.withHtml.r({ price: 1000 })}

			HTML: {translates.withPlural({ count: 3 })}
		</div>
	);
}
```

### <a name="TranslatesUpdate"></a>Как обновить переводы?

1. Отведите ветку от dev
2. `npm run tanker:download`, и если из танкера пришли изменения переводов, порезолвать конфликты, пробежаться глазами.
3. `npm run tanker:upload`, загрузить в танкер все новые ключи
4. Прийти к @tocher или @weidenbaum и попросить завести задачу на переводчиков и редакторов
5. Подождать.
6. `npm run tanker:download`, проверить новые переводы и изменения
7. Сделать пулл реквест, предупредить коллег в чате Frontend-а о новых переводах и дать 24 часа просмотреть заинтересованным.
8. Обязательно проверить переводы с тегами, чтобы не сломалось все!


### <a name="TranslatesRemoveUnused"></a>Как удалить неиспользуемые ключи из танкера?

1. Скачайте последнюю версию командой `gulp tanker:download`
2. Проверьте корректность переводов
3. Запустите командой `gulp tanker:replace`

**Внимание!** Команда `gulp tanker:replace` производит замещение кейсета, т.к. ключи, которых нет локально будут удалены из танкера.
Если передать пустой кейсет, то удалятся только ключи, кейсет нужно будет удалять вручную.

Возможные проблемы:

- не запустили `gulp tanker:download` и скрипт не разрешает выполнить замену ключей
- пока проверяли переводы в танкере что-то поменялось, тогда снова вернуться к п. 1


### <a name="TranslatesRollback"></a>Как откатить переводы?

1. Найдите нужную ревизию по адресу https://tanker.yandex-team.ru/~history/?project=pdb&branch=master
2. Запустите команду `gulp tanker:rollback --ref <revision-hash>`


### <a name="OAuth"></a>OAuth для переводов

Создайте файл в корне проекта `oauth.json` со следующим содержанием:

```json
{
    "tanker": "YOUR_TOKEN"
}
```

Для танкера токен можно получить [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=bbb4cb8bfac744afbeb539375be80a72)


<a name="Counters"></a>Счетчики
========

Все счетчики описаны в файле [counters.tsx](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections/src/counters/counters.ts)

Их полное описание находится в файле [countersDetails.ts](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections/src/counters/countersDetails.ts)

Формирование имен в счетчиках подчиняется следующим правилам:
1. Первая часть это тип события. Их должно быть ограниченное число, сейчас это `access`, `click`, `show`, `finish`. Их описание доступно на [wiki](https://wiki.yandex-team.ru/collections/logs/#tipydejjstvijj)
2. Вторая часть через точку - сущность, на которую направленно действие. Например `card`, `board`, `user`.
3. Третья часть это событие. Например, `share`.

Вторую и третью часть можно опускать при необходимости. Добавление четвертой и более частей должно иметь очень хорошее обоснование.

Рассмотрим типичный сценарий в терминах счетчиков. Например мы нажимаем на кнопку лайка:
1. `SendCounters.clickCardLike({...counters, cardId: card.id, is_liked: card.is_liked})`. Фиксируем нажатие на кнопку
2. `SendCounters.finishCardLike({...counters, cardId: card.id, is_liked: card.is_liked})`. Фиксируем окончания ajax запроса и успешный статус код

Для формирования параметров счетчика применяется семейство функций в объекте `Counters` с именами из `COUNTERS`. Таким образом для формирования параметров клика по карточке нужно использовать `Counters.clickCard({...params})`. Формирование параметров может быть полезно, если вы хотите использовать общий механизм кликов через дата аттрибуты. Если к любому тегу добавить аттрибут `data-c="параметры счетчика"`, то при клике на него будет автоматически отправлен счетчик. Этот способ **не рекомендуется**. Если у вас есть возможность отправлять счетчики из сервисов, то сделайте это там. Так как это можно протестировать юнит тестами.

Для отправки счетчиков применяется семейство функций `SendCounters` и логикой работы аналогичной `Counters`.

Для проброса параметров счетчиков через иерархию react компонентов используется компонент [Counter](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections/src/components/Counter/Counter.tsx). Его использование выглядит следующим образом:

```typescript jsx
import * as React from 'react';

import {Counter} from 'components/Counter/Counter';
import {CardLink} from 'components/Link/CardLink/CardLink';

export interface ComponentProps {
    cardId: string;
}

export function Component({cardId}: ComponentProps) {
    return (
        <Counter cardId={cardId} loc="header">
            <CardLink cardId={cardId} />
        </Counter>
    );
}
```

При этом компонент `CardLink` сможет получить доступ к параметрам счетчика внутри себя. Компонент `Counter` может вкладывать сам в себя, чтобы создавать слои параметров счетчиков. Получать параметры можно так:

```typescript jsx
import * as React from 'react';

import {counterConnect} from 'redux/connect';
import {CounterContext, SendCounters} from 'counters/counters';

export interface ComponentProps {

}

export const Component = counterConnect<ComponentProps>()(
    function Component({}: ComponentProps, {counter}: CounterContext) {
        return (
            <a
                href="/"
                onClick={() => SendCounters.clickCardLike({...counter})}
            />
        );
    }
);
```

Тестирование счетчиков производится юнит тестами. Общий механизм примерно такой:

```javascript
import details from 'counters/countersDetails';
import {resetCounters} from 'spec';

if (IS_CLIENT) {
    describe('Some test', function () {
        beforeEach(function () {
            resetCounters();
        });

        it('should work', function () {
            // do something

            expect(details.clickCardLike).to.be.met({
                cardId: '5a38f7bc5a7bb30093d25423',
                liked: 'true',
                loc: 'card'
            });
        });
    });
}
```

<a name="Svg"></a>Инлайн SVG (inline svg)
========

Инлайн svg иконок происходит с помощью [svg-react-loader](https://github.com/jhamlet/svg-react-loader) для всех файлов с расширением `*.inline.svg`
Список всех иконок можно посмотреть в сторибук, компонент Icons AllIcons

Внутрь можно пробрасывать любые пропсы, менять и т.д.
Имя импорта может быть любым, т.к. svg парсится через Object Tree и оборачивается как обычный React компонент с default export.

Иконки можно посмотреть тут https://pdb-storybook.n.yandex-team.ru/Icons/AllIcons

```typescript jsx
import MyIcon from 'components/Icons/icon.inline.svg';

<MyIcon props />
<MyIcon fill={'#000'} />
```

Также подключены иконки из `@yandex-serp-design/search`, которые можно посмотреть по [ссылке](https://lego.yandex-team.ru/search/icons/)

<a name="ServerDebugging"></a>Серверная отладка
=================

Добавьте к урлу параметр `inspect=1` и подключитесь Я.Бро или другим хромоподобным браузером к
сессии. Если автоматически не подхватило, то можно поискать тут [browser://inspect/#devices](browser://inspect/#devices)

Видео процесса https://jing.yandex-team.ru/files/ftdebugger/screencast_2018-02-27_23-35-19.mp4


<a name="BuildPlugins"/>Сборка плагинов
===============

Выкладка плагинов описана [здесь](https://wiki.yandex-team.ru/users/tocher/dobavlenie-ot-sashi/)

Сборка каждого плагина происходит отдельно для каждого бразуера.

### Chrome

    # localhost

    gulp build:chrome

    # l7test

    gulp build:chrome --env=testing

    # yandex.ru/collections

    gulp build:chrome --env=production

    # Pull request number

    PR=555 gulp build:chrome --env=testing

    # custom target host

    ORIGIN=https://menjoy-16425-ci1.si.yandex.ru gulp build:chrome --env=testing


<a name="Testing"/>Тестирование
============

### Визуальное тестирование компонент

В одной консоле выполняем

    gulp

В другой консоле запускаем тесты

    # Десктоп
    gulp e2e:gui -a --set desktop

    # Мобилка
    gulp e2e:gui -a --set mobile

Дополнительные опции:

    --retry 0 # отключаем ретраи
    --grep DesktopShareLayout # запускаем только нужные тесты
    --sandbox https://proxy.sandbox.yandex-team.ru/619359510/index.html # запускаем только упавшие тесты
    --from https://proxy.sandbox.yandex-team.ru/123456789/index.html # использует результат отчета из sandbox

Отладка тестов для визуального тестирования доступна по адресу ниже. Для отображения в браузере компонент для мобилок нужно передавать мобильный юзер-агент.

    https://localhost.yandex.ru:9002/%COMPONENT%


### E2E тестирование сценариев

В одной консоле выполняем

    E2E_MODE=yes gulp web

В другой консоле запускаем тесты

    # Десктоп
    gulp e2e:gui -a --set features:desktop

    # Мобилка
    gulp e2e:gui -a --set features:mobile

Для теста на локальном браузере нужно поставить `selenium-standalone`

    npm install -g selenium-standalone
    selenium-standalone install

И запустить

    selenium-standalone start
    IS_LOCAL_GRID=1 gulp e2e:gui -a --set features:desktop

Прогнать тест на стабильность локально
    `hermione_test_repeater_enabled=true gulp e2e:gui -a --set features:mobile --retry=0 --grep='Черновик' --repeat 10`

Для запуска заскипаных тестов, добавляйте параметр ISSUE_KEYS
    `ISSUE_KEYS='PODB-15585,PODB-15584,PODB-15594,PODB-18102' gulp e2e...`

Примеры и структура папок
    - [README](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections/e2e/features/README.md)

### Standalone режим гермионы

Если у вас не запущен проект и вы хотите просто запустить гермиона тесты, то можно использовать следующую команду:

    gulp e2e --set desktop

это работает как для e2e тестов, так и для визуально регрессионных.

### Jest тестирование

Запуск по платформам

    npm run jest:mobile
    npm run jest:desktop

Запуск в режиме watch

    npm run jest:mobile -- --watch

Построение покрытия

    npm run jest:mobile -- --coverage

<a name="BuildProduction"></a>Сборка для продакшена

    gulp release --production

<a name="Experiments"></a>Эксперименты
============

Экспериментный флаг заводится в два этапа:

1. Добавялем флаг в `Experiments`в файле [experiments.ts](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections/src/enums/experiments.ts). Название флага должно начинатся с префикса `FAVORITES_`
2. Добавляем описание флага в `EXPERIMENTS_DETAILS` в файл [experimentsDetails.ts](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/collections/src/enums/experimentsDetails.ts).
Все поля имеют функциональное применение, так что заполняйте честно.

*Использование флага*:

```typescript jsx
import * as React from 'react';

import {connect} from 'redux/connect';
import {State} from 'schema/state/State';
import {getExperiment} from 'dapamoga/common/getExperiment/getExperiment';
import Experiments from 'enums/experiments';

interface Internal {
    // 'true' - преобразуется в boolean
    // '1' - преобразуется в number
    // 'test' - останется строкой
    // Если нет дефолтов - то будет undefined
    hasMyExp: string | boolean | number | undefined;
}

function stateToProps(state: State): Internal {
    return {
        hasMyExp: getExperiment(state, Experiments.SERVER_REQUEST_TIMEOUT),
    };
}

export const Test = connect<{}, Internal>(stateToProps)(
    function Test({hasMyExp}: Internal) {
        return (
            <div>
                {hasMyExp ? 'On' : 'Off'}
            </div>
        );
    }
);
```

Раскатить флаг на 100% можно быстро через [ITS](https://nanny.yandex-team.ru/ui/#/its/locations/collections/nodejs/)

<a name="ReleaseCheckList"></a>Создание и выкатка релиза
==================
### Вводные
Директория в арке с sandbox-задачами https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/collections/

[Подробнее](./docs/deploy.md)

### Отведение релиза
- заходим по адресу https://a.yandex-team.ru/arc_vcs/frontend/docs/how-to/arc/setup-releases.md#отведение-релиза-из-ci
- отводим задачу для сервиса по описанному алгоритму
    1. переходим по адресу https://a.yandex-team.ru/projects/frontend/code/frontend/services/collections
    2. переходим на вкладку CI
    3. на вкладке Releases ищем Collections
    4. нажимаем кнопку `Run release`
    5. выбираем флоу, который хотим запустить. release-flow - для регулярных релизов, hotfix-flow - для хотфиксов
- запускается trendbox-job'a, которая запускает скрипты из package.json по этому флоу https://a.yandex-team.ru/arc/trunk/arcadia/frontend/.trendbox.yml?rev=r8849137#L176
- а он запускает npm скрипт `ci:deploy:release` https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/frontend-ci/legacy/trendbox/run-deploy.js?rev=r8704717#L72, который написан у нас в сервисе

### Раскатка на тестинг
1. Находим релизную задачу на борде https://st.yandex-team.ru/dashboard/60480
1. Пример задачи: https://st.yandex-team.ru/PODB-21484
1. Робот сам добавляет комментарий с задачами, которые были запущены [пример](https://st.yandex-team.ru/PODB-21484#61aba410cc8faa5da9572aaf)
1. Все задачи должны быть выполнены успешно (hermone:e2e надо актуализировать https://st.yandex-team.ru/PODB-21211). Если это не так, то нужно посмотреть на причины падения и или починить, или перезапустить
1. Заходим в любую job'у и переходим на sandbox-тикет типа TRENDBOX_CI_JOB_BETA
1. Переходим во вкладку с ресурсами. Там должны присутствовать ресурсы типа:
    - COLLECTIONS_FRONTEND_RESOURCE_PACKAGE (поедет на прод и prestable)
    - COLLECTIONS_FRONTEND_RESOURCE_TEST_PACKAGE (поедет на тестинг)
1. Копируем ссылку на ресурсы в релизный тикет, чтобы при раскатке не искать
1. Поменять ресурс в https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-test-yp/files на id `COLLECTIONS_FRONTEND_RESOURCE_TEST_PACKAGE` из таски `TRENDBOX_CI_JOB_BETA`
1. Зайти на https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-test-yp и прожать `change` (Перевести в `active`). Это зальет шаблоны релиза на L7
1. Поменять ресурс в https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-prestable-yp/files на id `COLLECTIONS_FRONTEND_RESOURCE_PACKAGE` из таски `TRENDBOX_CI_JOB_BETA`
1. Зайти на https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-prestable-yp и прожать `change` (Перевести в `active`). Это зальет шаблоны релиза на prestable
1. Поменять ресурс в https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-priemka-yp/files на id `COLLECTIONS_FRONTEND_RESOURCE_PACKAGE` из таски `TRENDBOX_CI_JOB_BETA`
1. Зайти на https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-priemka-yp и прожать `change` (Перевести в `active`). Это зальет шаблоны релиза на приемку
1. Дожидаемся, когда все сервисы перейдут в состояние `ACTIVE`
1. Проверяем работоспособность сервисов
    - https://collections-test.crowdtest.yandex.ru/collections/
    - https://pdb-prestable.n.yandex.ru/collections/
    - https://l7test.yandex.ru/collections/
1. Отдаем релиз в тестирование. Переводим релизный тикет в статус `Ready for Test`

### Раскатка на прод
1. Находим последний релизный ресурс `COLLECTIONS_FRONTEND_RESOURCE_PACKAGE` https://nda.ya.ru/t/51fCPkVj56L7L2 для задачи с типом `COLLECTIONS_FRONTEND_RELEASE`
1. Проверяем, что его MD5 совпадает с MD5 ресурса из пункта при раскатке релиза.
1. Переходим в задачу `COLLECTIONS_FRONTEND_RELEASE` и релизим ее. Жмем кнопку release (галку) в интерфейсе sandbox. Пример ссылки на задачу https://sandbox.yandex-team.ru/task/1307723984/view. После этого создается релиз на https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/pdb_production.
1. Открыть сервис https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/pdb_production/
1. Проверить, что в данный момент нет активных деплоев и сообщить в Collections DevOps чат о начале выкатки.
1. Нажать кнопку `deploy` и выбрать рецепт `deploy_pdb_nodejs_by_locations`
Или перейти по ссылке https://nda.ya.ru/3UVGV8 и выбрать рецепт.
1. После нажатия `deploy` покажется всплывающее окно, в нем удостовериться, что в сервисах указан верный id sandbox таски
1. После наливки первого ДЦ открываем yasm панель и кибану.
Наблюдаем около 5-10 минут (можно отфильтровать по версии и ДЦ), чтобы не было новых ошибок или других странностей.
    - YASM PDB_FRONT_TV - https://yasm.yandex-team.ru/panel/pdb_front_tv/
    - Kibana - https://pdb-kibana.n.yandex-team.ru/
    - Error booster - https://nda.ya.ru/t/z6H_s7tm3W3i6d выбираем слева новую версию, справа старую и смотрим новые ошибки
1. Если всё ок - жмём START, продолжают накатываться оставшиеся ДЦ.
1. После успешной выкатки сообщить в Collections DevOps чат, что выкатка сервиса завершена.
1. Закрыть релизную задачу

### Hotfix
- Стартуем с пункта `Как отвести релиз`, но выбираем hotfix

### Как доставляются ресурсы в няня-сервисы
На тестинг они доставляются руками, как написано в пункте `Раскатка на тестинг`
На прод они доставлюятся через механизм Ticket Integration
- почитать https://docs.yandex-team.ru/nanny/how-to/sandbox-integration#release-rules-matching-service
- настройка https://nanny.yandex-team.ru/ui/#/services/catalog/pdb-nodejs-production-man-yp/tickets_integration (смотреть на все три ДЦ)

## Заключение
- Некоторые дополнительные ссылки можно найти [здесь](./docs/anything.md)
- [Документация по асессорам](./assessors/readme.md)
- [Инфраструктура и деплой](./docs/deploy)
