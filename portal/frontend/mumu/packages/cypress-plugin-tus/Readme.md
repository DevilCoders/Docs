## Установка

1. `npm i --save-dev @yandex-int/cypress-plugin-tus`
2. Добавьте в plugins/index.ts
```ts

import {createTusPlugin} from '@yandex-int/cypress-plugin-tus';

export default function(on: Cypress.PluginEvents, config: Cypress.PluginConfigOptions) {
    createTusPlugin('morda', {env: 'prod'})(on);
    // tus consumer----^
    // какое окружение использовать --^
    //Варианты env: "prod" | "test" | "team" | "team-test" | "external"

};

```
3. Добавьте в support/commands.ts
```ts

// импорт добавляет команды в cy
import {setPrefix} from '@yandex-int/cypress-plugin-tus/commands';

/* Не обязательно, но можно установить
 * дефолтный префикс используемых логинов,
 * должен начинаться с yndx- или yandex-team-
 */
setPrefix('yndx-');

```

## Использование

Всего 2 команды

- `yaAuth(login: string, options?: {
    prefix?: string;
    tld?: string;
}): Cypress.Chainable;`

    Логинит переданым пользователем в указанном tld (по-умолчанию ru).

    Если не передан префикс, то используется установленный по умолчанию (смотрите выше).

- `yaLogout(opts?: {
    strict?: boolean;
    tld?: string;
}): Cypress.Chainable;`

    Разлогинивает пользователя в указанном tld (по-умолчанию ru).

    Если `strict === true` и пользователь не авторизован, то будет выброшена ошибка.