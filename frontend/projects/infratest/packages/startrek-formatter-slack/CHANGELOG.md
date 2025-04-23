# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [1.0.130](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.startrek-formatter-slack@1.0.130...@yandex-int/si.ci.startrek-formatter-slack@1.0.130) (2021-03-13)



## 1.0.130 (2021-03-12)



## 1.0.129 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 1.0.128 (2021-03-12)



## 1.0.127 (2021-03-09)



## 1.0.126 (2021-02-26)



## 1.0.125 (2021-02-09)



## [1.0.124](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.startrek-formatter-slack@1.0.123...@yandex-int/si.ci.startrek-formatter-slack@1.0.124) (2021-01-30)



## [1.0.123](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.startrek-formatter-slack@1.0.122...@yandex-int/si.ci.startrek-formatter-slack@1.0.123) (2021-01-29)



## [1.0.122](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.startrek-formatter-slack@1.0.121...@yandex-int/si.ci.startrek-formatter-slack@1.0.122) (2021-01-29)



## [1.0.121](https://github.yandex-team.ru/search-interfaces/infratest/compare/de255aef2b9a7cf24b8fd17a79115154438fda65...@yandex-int/si.ci.startrek-formatter-slack@1.0.121) (2021-01-29)


### Code Refactoring

* **startrek-formatter-slack:** create package ([de255ae](https://github.yandex-team.ru/search-interfaces/infratest/commit/de255aef2b9a7cf24b8fd17a79115154438fda65))


### BREAKING CHANGES

* **startrek-formatter-slack:** создание пакета

В конце концов уперлись в то, что в microservices не удается работать
с текущей версией si/ci, так как остались зависимости, присутствующие
в microservices, которые не были вынесены в пакеты и обращались через
относительные пути к пакетам, которые были переписаны на ts и не были
скомпилированы в случае если мы подключали si/ci как зависимость
в microservices.
