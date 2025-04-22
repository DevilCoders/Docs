# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [2.1.10](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.tracker-utils@2.1.10...@yandex-int/si.ci.tracker-utils@2.1.10) (2021-03-13)



## 2.1.10 (2021-03-12)



## 2.1.9 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 2.1.8 (2021-03-12)



## 2.1.7 (2021-03-09)



## [2.1.6](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.tracker-utils@2.1.5...@yandex-int/si.ci.tracker-utils@2.1.6) (2021-02-23)



## 2.1.5 (2021-02-09)



## [2.1.4](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.tracker-utils@2.1.3...@yandex-int/si.ci.tracker-utils@2.1.4) (2021-01-29)



## [2.1.3](https://github.yandex-team.ru/search-interfaces/infratest/compare/5bc9c15ac86020856ff9ef086749dfafd370dcfe...@yandex-int/si.ci.tracker-utils@2.1.3) (2021-01-29)


### Bug Fixes

* add missing `debug` dependency ([2a5558b](https://github.yandex-team.ru/search-interfaces/infratest/commit/2a5558b2ddb6acf30d9d50cb2f45683a9f0b63d5))


### Code Refactoring

* **tracker-utils:** change extractSpecialKey arguments order ([43ce771](https://github.yandex-team.ru/search-interfaces/infratest/commit/43ce77160988b16731990a61895c587bcb835697))


### Features

* **packages/tracker-utils:** добавит readme ([5b90a79](https://github.yandex-team.ru/search-interfaces/infratest/commit/5b90a794c75853a20ed12fba0a63d1d49976e0cc))
* **packages/tracker-utils:** перенесёт bug-tracker в пакеты ([5bc9c15](https://github.yandex-team.ru/search-interfaces/infratest/commit/5bc9c15ac86020856ff9ef086749dfafd370dcfe))
* **packages/tracker-utils:** сделает tracker-utils пакетом ([fa88387](https://github.yandex-team.ru/search-interfaces/infratest/commit/fa883877233c0aa7a37e7fb349a593631254003a))
* **packages/trascker-utils:** сделает изменения для увелечения версии ([94005d9](https://github.yandex-team.ru/search-interfaces/infratest/commit/94005d9ce83a0a26197a6e9839cd516e35fc1c42))
* **ramda-ext:** добавить функцию, проверяющую является ли строка числом ([0e066e8](https://github.yandex-team.ru/search-interfaces/infratest/commit/0e066e88f7ec9f384040657860e9b4e67928f279))
* **tracker-utils:** curry extractSpecialKey arguments ([55be75a](https://github.yandex-team.ru/search-interfaces/infratest/commit/55be75a0e7790e4995db192716dd5fcb3136f7cf))


### BREAKING CHANGES

* **tracker-utils:** * Проверка стала не чувствительна к регистру.
* Изменён порядок аргументов, нужно для облегчения проверки списка. Например, так
лучше каррировать и обойти массив строк.

ISSUE: FEI-17942
