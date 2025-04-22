# Тестирование

Тесты на фичи - в папке `features/messenger/<feature_name>/*.hermione.js`. Здесь `messenger` - это нэймспейс, который отделяет тесты на мессенджер (в которых есть дополнительные ассеты и плагины) от тестов на legacy-чаты и других проектов в этом репозитории.

## Unit

### Запуск Unit тестов:

`npm run test`.

### Написание Unit тестов

В Unit-тестах не проверяем вёрстку визуальных компонентов (для этого будет `Hermione assertView` + `Storybook`). Тестируем работу отдельных функций, работу событий, используя framework для тестирования [Jest](https://facebook.github.io/jest/)

## Тесты компонентов скриншотами через [Storybook](https://storybook.js.org) и [Hermione assertView](https://github.com/gemini-testing/hermione#assertview)

### Запуск

Перед запуском тестов соберите storybook командой `npm run storybook:build` (в CI сборка Storybook вызывается из Makefile)
Для запуска теста достаточно выполнить команду `npm run hermione:storybook <имя файла>` или `npm run hermione:storybook --grep "<имя story>"` (с save и play нам работать не надо) и проверить/сохранить полученные скриншоты.

### Написание тестов

Для компонента нужно создать файл `*.stories.tsx`, где отобразить нужные состояния компонента. Пример:

```jsx
import * as React from 'react';
import { storiesOf } from '@storybook/react';

import { MyComponent } from '.';

const stories = storiesOf('UI|MyComponent', module);

stories.add('default', () => <MyComponent />);
stories.add('label', () => <MyComponent label='some test' />);
```

Тест пишется в файле `*.hermione.js` рядом с файлом `*.stories.tsx`. Пример теста:

```js
specs({
    feature: 'UI|MyComponent', // указываем имя фичи как имя компонента из storybook
}, () => {
    it('default', async function () {
        const { browser } = this;
        // имя и вид компонента как в Storybook
        await browser.chatOpenComponent('UI|MyComponent', 'default');
        // ждём появления нужного селектора на странице
        await browser.waitForVisible('.my-component');
        // делаем скриншот с соответствующим названием
        await browser.assertView('UI|MyComponent default', '.my-component');
    });

    // отдельно делаем скриншот другого вида
    it('label', async function () {
        const { browser } = this;
        await browser.chatOpenComponent('UI|MyComponent', 'label');
        await browser.waitForVisible('.my-component');
        await browser.assertView('UI|MyComponent label', '.my-component');
    });
});
```

### Использование [Storybook Knobs](https://github.com/storybookjs/storybook/tree/master/addons/knobs) в тесте

```js
it('default', async function () {
    const { browser } = this;
    // имя и вид компонента как в Storybook, объект в формате { knobName: knobValue }
    await browser.chatOpenComponent('UI|MyComponent', 'default', {
        text: 'Text',
        boolean: true,
        number: 1,
        array: [],
    });
    // ждём появления нужного селектора на странице
    await browser.waitForVisible('.my-component');
    // делаем скриншот с соответствующим названием
    await browser.assertView('UI|MyComponent default', '.my-component');
});
```

## [Hermione] на фичи

### Запуск [Hermione] тестов

Перед использованием нужно [установить](https://vault-api.passport.yandex.net/docs/#cli) клиент [секретницы](https://yav.yandex-team.ru/). При ошибке `error: RSA keys not found` нужно выполнить команду `ssh-add`.

Перед запуском тестов надо выполнить сборку:
```
npm run build:dev
```

Доступные команды для запуска hermione тестов (в package.json можно подробно посмотреть какая команда что делает):
- `npm run hermione:local` - запуск тестов в удаленном гриде
- `npm run hermione:local-debug` - запуск тестов в локальном гриде в chrome-desktop в режиме --inspect. Позволяет дебажить прогон тестов. Должен быть установлен и запущен selenium-standalone. Подробно о том как это сделать - [здесь](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#lokalnyjjgridselenium-standalone)
- `npm run hermione:debug` - запуск тестов в удаленном гриде в дебаг режиме. Позволяет посмотреть через vnc как тест прогоняется на удаленной машинке

Эти команды из секретницы достают токен тестового пользователя (права на секрет у сервиса [Web мессенджер](https://abc.yandex-team.ru/services/mssngr-ui/)), с которым мессенджер в тестах ходит в бэкенд (в тестах используется авторизация по токену, а не по кукам)

Параметры [CLI](https://github.com/gemini-testing/hermione#cli) в команду передаются после `--`, например:
```
npm run hermione:local -- tests/hermione/suites/messenger/open-by-url/open-by-url.chamb.desktop.hermione.ts --play --retry 0 -b chrome-desktop
```

Hermione-тесты выполняются на записанных ответах бэкенда по HTTP и WebSocket. Параметры командной строки `--save` и `--play` указывают на то, записываем мы дампы или воспроизводим. Если ни один из параметров не задан, по умолчанию используется `--play`. Запись дампов нужно выполнять с браузером `-b chrome-desktop` - для остальных браузеров настроено брать дампы для этого браузера.

Также в режиме `--play` возможен запуск графического интерфейса для анализа визуальной разницы выполнения тестов на скриншотах, например:
```
npm run hermione:local -- gui features/messenger/open-by-url/open-by-url.chamb.desktop.hermione.ts --play --retry 0 -b chrome-desktop
```

### Информация по аккаунтам в секретнице

В секретнице, кликнув на алиас **MESSENGER_EXTERNAL_TEST**, можно обнаружить 2 типа аккаунтов:

- `MESSENGER_EXTERNAL_TEST_LOGIN` - аккаунты с неподтвержденным номером телефона
- `YNDX_MSSNGR_TST_1_LOGIN` - аккаунты с подтвержденным номером телефоном (в основном именно они используются для тестирования)

Всего создано 5 тестовых аккаунтов второго типа. Все они заканчиваются индексом (1-5), и все имеют одинаковый пароль. Аккаунт, под которым непосредственно гоняются сами тесты, имеет индекс 1.

### Assets подключаемые при прогонах hermione тестов

Лежат в `.config/kotik/middlewares/test-assets/`. Среди них стоит обратить внимание на `index.css`, в которых переопределены некоторые селекторы приложения. Так например для предотвращения мигания тостов об ошибках в тестах `.yamb-toast` прописано свойство `display:none`

### Написание [Hermione] тестов

Hermione тесты пишутся на "фичи", а не на отдельные компоненты, поэтому находятся в папке `features/messenger/<feature_name>/<test_name>.{common, desktop, touch-phone}.hermione.js` . В имени файла __обязательно__ указывается платформа, на которой должен запуститься тест: `common`, `desktop` или `touch-phone`. Рядом с кодом теста лежит файл `<test_name>.<platform>.yml` - тестовый сценарий на естественном языке. Содержание тестов должно соответствовать тестовому сценарию, который пишется совместно с тестировщиком. В коде тестов используется команды тестового фреймворка [webdriver.io](http://v4.webdriver.io/api.html) а также команды, написанные в нашем репозитории [/hermione/commands].
_Примечание_**: иногда имена команд из документации к `webdriver.io` и тех, что используются в `hermione` не совпадают (например `moveTo()` в `webdriver.io` -> `moveToObject(selector)` в `hermione`). В этом случае можно поискать команду со схожим названием в репозитории web4.

Для создания css селекторов, которые используются командами hermione юзаем `bem-page-object`:
- [Документация](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/bem-page-object)
- [Пример использования](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/services/tutor/tests/hermione/page-objects/elems.js)

#### Команда yaOpenMessenger

Открывает мессенджер.

Опционально можно выбрать чат, с которым нужно открыть диалог с помощью параметра `guid`, с помощью алиаса `alias` или параметра `chatId` (см [hermione/commands/yaOpenMessenger.ts]).

Все новые тесты рекомендуется писать с использованием `async/await`.

#### Тесты с общением двух и более пользователей

Записать дампов с общением двух пользователей производиться в полуавтоматическом режиме: нужно в браузере на рабочем компьютере залогиниться пользователем `yndx-mssngr-tst-2` (пароль есть в секретнице) и в чате с ним выполнять нужные действия в hermione (как пример автоматизация [features/messenger/receiving-messages/receiving-messages.common.hermione.ts])

#### Пример теста

```
specs({
    feature: 'Открытие чата по ссылке'
}, function () {
    it('Открывается чат по ссылке', async function () {
          // сделаем более удобную для использования переменную
          const { browser } = this;

          // Открыть мессенджер и чат с пользователем с guid 'ef212763-afac-488b-b099-f0e1c23cba3d'
          await browser.yaOpenMessenger({
            guid: 'ef212763-afac-488b-b099-f0e1c23cba3d'
          })
          // Проверить, что видны необходимые элементы чата
          await browser.waitForVisible('.yamb-sidebar', 'Не показался список чатов');
          await browser.waitForVisible('.yamb-chat-list-item', 'В списке чатов нет ни одного чата');
          await browser.waitForVisible('.yamb-chat', 'Чат не открылся');
          // Вставить текст в поле ввода
          await browser.setValue('.ui-textarea__control', 'text');
          // Нажать кнопку "Отправить"
          await browser.click('.yamb-compose__button_submit');
          // Проверить, что сообщение появилось в списке отправленных
          await browser.waitForVisible('.yamb-message-text');
    });
});

```
### Просмотр дампов

Если вдруг появилась необходимость заглянуть в дамп, можно сделать это с помощью следующего скрипта
(все опции можно посмотреть в его исходниках):
```
node scripts/dump-analizer.js features/messenger/open-by-url/test-data/86d4542/5bf2dab043c155e86c7a.json.gz
--pretty
```
Вывод:
```
{
  status: 'ok',
  data: {
    user: {
      guid: '84e2c95f-7a61-42d4-a546-c3c9c3ae0397',
      display_name: 'yndx-mssngr-tst-1 a.',
      registration_status: 'U',
      version: 1580735792419387,
      phone_id: '57cbceab-ebe4-4d04-8fec-1bd3cb664e1d'
,
      suspicion_version: 0,
      uid: 863631190,
      phone: '+70000972868',
      contacts: []
    }
  },
  testRunId: 'NDFhZjFkMi9jaHJvbWUtZGVza3RvcCwxNTgwNzM1
Nzg1OTI2LGZlYXR1cmVzL21lc3Nlbmdlci9vcGVuLWJ5LXVybC90ZX
N0LmRlc2t0b3AuaGVybWlvbmUuanMsODZkNDU0Mg=='
}
```
Можно также посмотреть, для какого теста записан дамп (данная опция не работает для дампов,
которые были записаны до того, как она появилась - лечится перезаписыванием дампов для теста):
```
node scripts/dump-analizer.js features/messenger/open-by-url/test-data/86d4542/5bf2dab043c155e86c7a.json.gz
--show
```
Вывод:
```
Test with 86d4542 hash for current dump is in features/messenger/open-by-url/test.desktop.hermione.js
```

Полезные ссылки:
* [Документация Webdriver](http://v4.webdriver.io/api.html)
* [Документация Selenium](http://selenium2.ru/docs.html)
* [Установка и подключение Selenium-сервера](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/installselenium)
* [Известные проблемы](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/e2e-wd/seleniumexception)
* [Документация Hermione](https://github.com/gemini-testing/hermione)
* [Пост в Этушке о снятии скриншотов в Hermione](https://clubs.at.yandex-team.ru/search-interfaces-serp/1635)
* [Гайд по разработке hermione-тестов](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/e2e-wd#lokalnyjjzapusk)
* [Практики разработки hermione-тестов](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/reliabletests)
* [Функциональное тестирование интерфейсов](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/)
* [Общий гайд по unit-тестированию](https://wiki.yandex-team.ru/search-interfaces/testing/unit-test-guidelines/)
* [Практики написания hermione-тестов fiji](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/hermione/readme.md)


## Сценарии тестирования в YML

[Документация palmsync][Palmsync]

[Документация manual-runs][manual-runs]

Инструкция для тестировщиков [Как подготовить окружение и писать yml](https://wiki.yandex-team.ru/test/serp/Stazhirovka/Chek-list-stazhirovki-v-SERPe/yml/)

Тестовые сценарии хранятся в `*.testpalm.yml`-файлах в папке [features](./features) и
синхронизируются с проектом [chat](https://testpalm.yandex-team.ru/chat) на сервисе TestPalm.

Валидация правильности заполнения файлов с тестовыми сценариями и их синхронизация выполняются инструментом [Palmsync].

[Palmsync] для проекта настроен через конфигурационный файл [`.palmsync.conf.js`].
Он содержит настройки [Palmsync], специфичные для проекта. Подробнее о структуре конфигурационного файла можно прочитать
в документации [Palmsync] [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync#конфигурация-с-помощью-файла-palmsyncconfjs).

Кроме этого у нас поддержаны [Импортируемые группы шагов](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync/docs/steps-group.md), a.k.a shared steps

Для vs-code доступно расширение [Tide](https://github.yandex-team.ru/search-interfaces/tide), помогающее в написании `testpalm.yml` файлов

## Кастомные поля проекта

О том, как настраивать кастомные поля, можно прочитать в документации [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync#schemeextension).
Настроенные в настоящий момент кастомные поля перечислены ниже.

### v-team

Ответственная команда.

Допустимые значения можно увидеть в описании этого поля в конфигурационном файле [Palmsync] - [`.palmsync.conf.js`].

### browsers

Список браузеров, для которых актуален сценарий. На проекте добавлена валидация поля: каждое значение, указанное в поле,
должно быть одним из названий браузеров, описанных в [`.config/browsers.js`].

В остальном полностью соответствует описанию поля в [общей схеме](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync#browsers).

### files

**Обязательное.**

В остальном полностью соответствует описанию поля в [общей схеме](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync#files).

### manager

**Обязательное.**

В остальном полностью соответствует описанию поля в [общей схеме](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync#manager).

### qa-engineer

**Обязательное.**

В остальном полностью соответствует описанию поля в [общей схеме](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/palmsync#qa-engineer).

## Настройка ручных ранов

Ручные раны формируются при помощи инструмента [manual-runs].

Создаваемые раны настраиваются в конфигурационном файле [`.manual-test-runs.conf.js`].
Подробнее о структуре конфигурационного файла можно прочитать в документации [manual-runs] [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/manual-test-runs#конфигурация-с-помощью-файла-manualtestrunsconfjs).

О том, как настраивать ручные раны для проекта, можно прочитать в документации [manual-runs] [здесь](https://github.yandex-team.ru/search-interfaces/infratest/blob/master/packages/manual-test-runs#runs).

В проекте сейчас настроены раны для каждого поддерживаемого браузера - настроены в файле [`.config/browsers.js`].

[Hermione]: https://github.com/gemini-testing/hermione
[Palmsync]: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/palmsync
[manual-runs]: https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/manual-test-runs

[`.palmsync.conf.js`]: ./.palmsync.conf.js
[`.manual-test-runs.conf.js`]: ./.manual-test-runs.conf.js
[`browsers.js`]: ./.config/browsers.js
