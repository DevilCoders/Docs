# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [2.1.28](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.27...@yandex-int/si.ci.genisys-local-config@2.1.28) (2021-04-22)

**Note:** Version bump only for package @yandex-int/si.ci.genisys-local-config





## [2.1.27](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.26...@yandex-int/si.ci.genisys-local-config@2.1.27) (2021-04-19)

**Note:** Version bump only for package @yandex-int/si.ci.genisys-local-config





## [2.1.26](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.25...@yandex-int/si.ci.genisys-local-config@2.1.26) (2021-03-23)

**Note:** Version bump only for package @yandex-int/si.ci.genisys-local-config





## [2.1.25](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.24...@yandex-int/si.ci.genisys-local-config@2.1.25) (2021-03-19)

**Note:** Version bump only for package @yandex-int/si.ci.genisys-local-config





## [2.1.24](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.23...@yandex-int/si.ci.genisys-local-config@2.1.24) (2021-03-15)

**Note:** Version bump only for package @yandex-int/si.ci.genisys-local-config





## [2.1.23](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.22...@yandex-int/si.ci.genisys-local-config@2.1.23) (2021-03-14)

**Note:** Version bump only for package @yandex-int/si.ci.genisys-local-config





## [2.1.22](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.1.22...@yandex-int/si.ci.genisys-local-config@2.1.22) (2021-03-13)



## 2.1.22 (2021-03-12)



## 2.1.21 (2021-03-12)



## 2.1.20 (2021-03-12)



## 2.1.19 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 2.1.18 (2021-03-12)



## 2.1.17 (2021-03-11)



## 2.1.16 (2021-03-10)



## 2.1.15 (2021-03-10)



## 2.1.14 (2021-03-10)



## 2.1.13 (2021-03-10)



## 2.1.12 (2021-03-09)



## 2.1.11 (2021-03-09)



## 2.1.10 (2021-02-26)



## 2.1.9 (2021-02-17)



## 2.1.8 (2021-02-17)



## 2.1.7 (2021-02-10)



## 2.1.6 (2021-02-10)



## 2.1.5 (2021-02-09)



## 2.1.4 (2021-02-09)



## 2.1.3 (2021-01-28)



## 2.1.2 (2021-01-28)



## 2.1.1 (2021-01-26)



# 2.1.0 (2021-01-26)


### Features

* add missing packages and adjust versions ([3517486](https://github.yandex-team.ru/search-interfaces/infratest/commit/3517486e013aa8958cdfba9896bcdd1f6da1e891))



## [2.0.3](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.0.2...@yandex-int/si.ci.genisys-local-config@2.0.3) (2021-01-22)



## [2.0.2](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.0.1...@yandex-int/si.ci.genisys-local-config@2.0.2) (2021-01-19)



## [2.0.1](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.genisys-local-config@2.0.0...@yandex-int/si.ci.genisys-local-config@2.0.1) (2021-01-18)


### Bug Fixes

* **package:** fix repository url ([f785e7c](https://github.yandex-team.ru/search-interfaces/infratest/commit/f785e7c000af0b3e5a24362357ea5653e96a06f4))



# [2.0.0](https://github.yandex-team.ru/search-interfaces/infratest/compare/03d6eda4bfa3570d5009a0377aea9b33fc35acd9...@yandex-int/si.ci.genisys-local-config@2.0.0) (2021-01-18)


### Code Refactoring

* **genisys-local-config:** create package ([03d6eda](https://github.yandex-team.ru/search-interfaces/infratest/commit/03d6eda4bfa3570d5009a0377aea9b33fc35acd9))


### BREAKING CHANGES

* **genisys-local-config:** создание пакета

В конце концов уперлись в то, что в microservices не удается работать
с текущей версией si/ci, так как остались зависимости, присутствующие
в microservices, которые не были вынесены в пакеты и обращались через
относительные пути к пакетам, которые были переписаны на ts и не были
скомпилированы в случае если мы подключали si/ci как зависимость
в microservices.
