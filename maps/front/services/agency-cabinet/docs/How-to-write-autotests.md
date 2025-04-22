# Как писать функциональные тесты

## Общие сведения

Для запуска функциональных тестов используется пакет [Pup](https://a.yandex-team.ru/arcadia/maps/front/packages/pup) - надстройка над [Jest](https://jestjs.io/) и [Puppeteer](https://github.com/puppeteer/puppeteer).

Все функциональные тесты расположены в папке `tests/func`, логически бьются на страницы/компоненты.

Типичные команды-обертки над Puppeteer API вынесены в `tests/func/utils/commands.ts`.

CSS селекторы для тестов хранится в файле `tests/func/common/css-selectors.ts`, у каждого селектора должно быть свое человекочитаемое описание в `tests/func/common/selectors-description.ts`. Пример:
```ts
// css-selectors.ts
{
    auth: {
        profileInfo: '.profile'
    }
};


// selectors-description.ts
{
    [CSS_SELECTORS.auth.profileInfo]: {
        description: 'Profile info block'
    }
};
```

## Написание теста

Для написания тестов используются стандартные средства [Jest](https://jestjs.io/) и [Puppeteer](https://github.com/puppeteer/puppeteer). Зачастую в тесте следует залогиниться. Для удобства метод `openPage` принимает параметр `auth`, куда можно передать учетные данные для залогина. Тестовые учетки с разными пользовательскими ролями можно найти в файле `/agency-cabinet/tests/func/common/users.ts`.
Пример теста:
```ts
describe('Login', () => {
    test(`should shown logo after login by ${UserRole.ADMIN}`, async () => {
        await openPage({pathname: `/`, auth: USERS_BY_ROLE[UserRole.ADMIN]});
        await page.waitForSelector(cssSelectors.logo);
    });
});
```

_**Важно!**_

`@yandex-int/tests-to-testpalm` не умеет работать с Jest.each. Все подобные конструкции следует заменить на цикл while/for.

----

## Как запустить тесты

Прогон тестов автоматически запускаются в CI на каждый пулл-реквест и тэг в транке. Для запуска тестов на локальной машинке необходимо выполнить `STAND_URL=SOME_STAND_URL npm run test:func`, где SOME_STAND_URL - урл стенда или алиас на локалхост. Для запуска отдельного файла или дирректории передаем путь в параметр `match`:

`STAND_URL=SOME_STAND_URL npm run test:func -- --match=./tests/func/somepath/`

Для первичной записи или обновления моков необходино передать флаг `--record`:

`STAND_URL=SOME_STAND_URL npm run test:func -- --record`

Для прогона теста внутри Docker-контейнера следует использовать флаг `--engine=docker`:

`STAND_URL=SOME_STAND_URL npm run test:func -- --engine=docker`

При запуске теста на локальной машине (с `--engine=local`) возможно прогнать тесты в "headfull" режиме. Режим позволяет отследить все происходящее в браузере. Для этого существует флаг `--debug`:

`STAND_URL=SOME_STAND_URL npm run test:func -- --debug`

_**Следует помнить**_

Задержку между действиями браузера в `debug` режиме можно контролировать из конфига для Pup `tests/func/pup.config.ts` настройкой `slowMo?: number`.

----

## Генерация описания тесткейса

Генерация описания запускаются в CI на каждый пулл-реквест. Синхронизируется с [Testpalm](https://testpalm.yandex-team.ru/) происходит на тэг в транке. Для того, чтобы сгенерировать описание локально и увидеть разницу локальной версии и версии из Testpalm необходимо выполнить `MODE=dry-run npm run sync-testcases`. Отчет можно будет найти по пути `tests/func/reports/index.html`. Подробная информация о пакете `@yandex-int/tests-to-testpalm` по [ссылке](https://a.yandex-team.ru/arcadia/maps/front/packages/tests-to-testpalm).
