# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [1.0.147](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.146...@yandex-int/si.ci.github-formatter-slack@1.0.147) (2021-04-22)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.146](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.145...@yandex-int/si.ci.github-formatter-slack@1.0.146) (2021-04-19)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.145](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.144...@yandex-int/si.ci.github-formatter-slack@1.0.145) (2021-04-19)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.144](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.143...@yandex-int/si.ci.github-formatter-slack@1.0.144) (2021-04-08)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.143](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.142...@yandex-int/si.ci.github-formatter-slack@1.0.143) (2021-03-25)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.142](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.141...@yandex-int/si.ci.github-formatter-slack@1.0.142) (2021-03-23)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.141](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.140...@yandex-int/si.ci.github-formatter-slack@1.0.141) (2021-03-19)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.140](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.139...@yandex-int/si.ci.github-formatter-slack@1.0.140) (2021-03-15)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.139](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.138...@yandex-int/si.ci.github-formatter-slack@1.0.139) (2021-03-14)

**Note:** Version bump only for package @yandex-int/si.ci.github-formatter-slack





## [1.0.138](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.138...@yandex-int/si.ci.github-formatter-slack@1.0.138) (2021-03-13)



## 1.0.138 (2021-03-12)



## 1.0.137 (2021-03-12)



## 1.0.136 (2021-03-12)



## 1.0.135 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 1.0.134 (2021-03-12)



## 1.0.133 (2021-03-11)



## 1.0.132 (2021-03-10)



## 1.0.131 (2021-03-10)



## 1.0.130 (2021-03-10)



## 1.0.129 (2021-03-10)



## 1.0.128 (2021-03-09)



## 1.0.127 (2021-03-09)



## 1.0.126 (2021-03-01)



## 1.0.125 (2021-02-26)



## 1.0.124 (2021-02-26)



## 1.0.123 (2021-02-26)



## 1.0.122 (2021-02-26)



## 1.0.121 (2021-02-23)



## 1.0.120 (2021-02-23)



## 1.0.119 (2021-02-21)



## 1.0.118 (2021-02-09)



## 1.0.117 (2021-01-30)


### Bug Fixes

* update @yandex-int/si.ci.formatter-slack ([637b22a](https://github.yandex-team.ru/search-interfaces/infratest/commit/637b22ac9eb1007dd578e400e10466b9a993bdae))



## 1.0.116 (2021-01-30)



## [1.0.115](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.github-formatter-slack@1.0.114...@yandex-int/si.ci.github-formatter-slack@1.0.115) (2021-01-30)



## [1.0.114](https://github.yandex-team.ru/search-interfaces/infratest/compare/7290cdc3a7485d4e81f1242516020e50da80e561...@yandex-int/si.ci.github-formatter-slack@1.0.114) (2021-01-30)


### Code Refactoring

* **github-formatter-slack:** create package ([7290cdc](https://github.yandex-team.ru/search-interfaces/infratest/commit/7290cdc3a7485d4e81f1242516020e50da80e561))


### BREAKING CHANGES

* **github-formatter-slack:** создание пакета

В конце концов уперлись в то, что в microservices не удается работать
с текущей версией si/ci, так как остались зависимости, присутствующие
в microservices, которые не были вынесены в пакеты и обращались через
относительные пути к пакетам, которые были переписаны на ts и не были
скомпилированы в случае если мы подключали si/ci как зависимость
в microservices.
