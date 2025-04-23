# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [2.0.44](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.43...@yandex-int/si.ci.sandbox-formatter-html@2.0.44) (2021-04-22)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.43](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.42...@yandex-int/si.ci.sandbox-formatter-html@2.0.43) (2021-04-19)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.42](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.41...@yandex-int/si.ci.sandbox-formatter-html@2.0.42) (2021-03-30)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.41](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.40...@yandex-int/si.ci.sandbox-formatter-html@2.0.41) (2021-03-23)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.40](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.39...@yandex-int/si.ci.sandbox-formatter-html@2.0.40) (2021-03-19)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.39](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.38...@yandex-int/si.ci.sandbox-formatter-html@2.0.39) (2021-03-15)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.38](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.37...@yandex-int/si.ci.sandbox-formatter-html@2.0.38) (2021-03-14)

**Note:** Version bump only for package @yandex-int/si.ci.sandbox-formatter-html





## [2.0.37](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.sandbox-formatter-html@2.0.37...@yandex-int/si.ci.sandbox-formatter-html@2.0.37) (2021-03-13)



## 2.0.37 (2021-03-12)



## 2.0.36 (2021-03-12)



## 2.0.35 (2021-03-12)



## 2.0.34 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 2.0.33 (2021-03-12)



## 2.0.32 (2021-03-11)



## 2.0.31 (2021-03-10)



## 2.0.30 (2021-03-10)



## 2.0.29 (2021-03-10)



## 2.0.28 (2021-03-10)



## 2.0.27 (2021-03-09)



## 2.0.26 (2021-03-09)



## 2.0.25 (2021-02-26)



## 2.0.24 (2021-02-26)



## 2.0.23 (2021-02-24)



## 2.0.22 (2021-02-23)



## 2.0.21 (2021-02-20)



## 2.0.20 (2021-02-17)



## 2.0.19 (2021-02-17)



## 2.0.18 (2021-02-10)



## 2.0.17 (2021-02-10)



## 2.0.16 (2021-02-09)



## 2.0.15 (2021-02-09)



## 2.0.14 (2021-02-02)



## 2.0.13 (2021-02-01)



## 2.0.12 (2021-01-31)



## 2.0.11 (2021-01-30)


### Bug Fixes

* update @yandex-int/si.ci.formatter-html ([4b2ebc9](https://github.yandex-team.ru/search-interfaces/infratest/commit/4b2ebc9a201a322006e8cf28d04a47ea5421e974))



## 2.0.10 (2021-01-28)



## 2.0.9 (2021-01-28)



## 2.0.8 (2021-01-28)



## 2.0.7 (2021-01-28)



## 2.0.6 (2021-01-27)



## 2.0.5 (2021-01-26)



## 2.0.4 (2021-01-26)



## 2.0.3 (2021-01-15)


### Bug Fixes

* legacy-test-toolchain deps in tests ([514f555](https://github.yandex-team.ru/search-interfaces/infratest/commit/514f5554999f52100d3dbc4c7b5ba20f949b7412))



## 2.0.2 (2020-12-29)



## 2.0.1 (2020-12-28)



# [2.0.0](https://github.yandex-team.ru/search-interfaces/infratest/compare/cf87ad977754cd254f8f8d0b2577dc6a5ca3ad78...@yandex-int/si.ci.sandbox-formatter-html@2.0.0) (2020-12-25)


### Code Refactoring

* **sandbox-formatter-html:** create package ([cf87ad9](https://github.yandex-team.ru/search-interfaces/infratest/commit/cf87ad977754cd254f8f8d0b2577dc6a5ca3ad78))


### BREAKING CHANGES

* **sandbox-formatter-html:** создание пакета

В конце концов уперлись в то, что в microservices не удается работать
с текущей версией si/ci, так как остались зависимости, присутствующие
в microservices, которые не были вынесены в пакеты и обращались через
относительные пути к пакетам, которые были переписаны на ts и не были
скомпилированы в случае если мы подключали si/ci как зависимость
в microservices.
