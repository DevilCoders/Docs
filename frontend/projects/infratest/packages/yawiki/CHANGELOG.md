# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [1.2.38](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.yawiki@1.2.38...@yandex-int/si.ci.yawiki@1.2.38) (2021-03-13)



## 1.2.38 (2021-03-12)



## 1.2.37 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 1.2.36 (2021-03-12)



## 1.2.35 (2021-03-09)



## 1.2.34 (2021-02-09)



## 1.2.33 (2021-01-28)



## 1.2.32 (2021-01-28)



## 1.2.31 (2021-01-26)



## 1.2.30 (2021-01-26)



## 1.2.29 (2021-01-15)


### Bug Fixes

* legacy-test-toolchain deps in tests ([514f555](https://github.yandex-team.ru/search-interfaces/infratest/commit/514f5554999f52100d3dbc4c7b5ba20f949b7412))



## 1.2.28 (2020-12-29)



## 1.2.27 (2020-12-25)



## [1.2.26](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.yawiki@1.2.25...@yandex-int/si.ci.yawiki@1.2.26) (2020-12-25)



## [1.2.25](https://github.yandex-team.ru/search-interfaces/infratest/compare/cb5cd389999dca8a66a2c6bbd5251a99f61eefc5...@yandex-int/si.ci.yawiki@1.2.25) (2020-12-25)


### Bug Fixes

* **yawiki:** использовать REST API ([cb5cd38](https://github.yandex-team.ru/search-interfaces/infratest/commit/cb5cd389999dca8a66a2c6bbd5251a99f61eefc5))


### Features

* **yawiki:** updatePage ([4ea38d3](https://github.yandex-team.ru/search-interfaces/infratest/commit/4ea38d3d921ebc1037576d2a8609d2f390d82bb2))


### BREAKING CHANGES

* **yawiki:** * Для авторизации требуется token, вместо связки логин + пароль.
* API: для создания инстанса вместо класса используется фабрика.

Refactor:
* Использовал `got`, вместо `q-io`.
* Использовал нативные промисы.
