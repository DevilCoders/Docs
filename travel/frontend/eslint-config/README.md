# @yandex-travel/eslint-config

[![npm version](https://badger.yandex-team.ru/npm/@yandex-travel/eslint-config/version.svg)](https://npm.yandex-team.ru/@yandex-travel/eslint-config)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/eslint-config&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/eslint-config)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/eslint-config&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/eslint-config)
[![distribution health](https://badger.yandex-team.ru/oko/pkg/@yandex-travel/eslint-config/health.svg)](https://oko.yandex-team.ru/pkg/@yandex-travel/eslint-config)

## Usage

```
npm i --save-dev @yandex-travel/eslint-config
```

In your .eslintrc

```
{
   extends: [
       // For whole project
       "@yandex-travel/eslint-config/base",
       // For node server
       "@yandex-travel/eslint-config/server",
       // For react client
       "@yandex-travel/eslint-config/client",
   ]
   ...
}
```

## Themes to discuss

-   @typescript-eslint/member-ordering - discuss about order: all private, all protected, all public

-   @typescript-eslint/explicit-member-accessibility - problem with DeadCode

```
'@typescript-eslint/explicit-member-accessibility': [
    ERROR,
    {accessibility: 'explicit'},
],
```

-   Check for missing jsx/tsx in filesheck (use js/ts instead of jsx/tsx)

    -   Profit: `react/sort-comp` - check tsx files, `@typescript-eslint/member-ordering` check ts files. In first case we check react without react.s

-   Add config for tools - scripts, tools and other, that run only for build and prepare project. This is not runtime code and therefore do not need security (frigga, i18n-ts, holydays, custom webpack loaders, ...)

    -   Are there any differences from /base?

-   Add config for tests (jest, ...)

## Plan

-   Think about `@typescript-eslint/recommended`
-   camelcase - change level to ERROR, ignore API directories
