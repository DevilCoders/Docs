# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [3.0.11](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.requests@3.0.11...@yandex-int/si.ci.requests@3.0.11) (2021-03-13)



## 3.0.11 (2021-03-12)



## 3.0.10 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 3.0.9 (2021-03-12)



## 3.0.8 (2021-03-09)



## 3.0.7 (2021-02-09)



## 3.0.6 (2021-01-28)



## 3.0.5 (2021-01-28)



## 3.0.4 (2021-01-26)



## 3.0.3 (2021-01-26)


### Bug Fixes

* **requests:** adjust test timeout ([d4ff931](https://github.yandex-team.ru/search-interfaces/infratest/commit/d4ff9314629ecbf9dcb88f8b224906e96703cf2a))



## 3.0.2 (2021-01-15)


### Bug Fixes

* legacy-test-toolchain deps in tests ([514f555](https://github.yandex-team.ru/search-interfaces/infratest/commit/514f5554999f52100d3dbc4c7b5ba20f949b7412))



## 3.0.1 (2020-12-29)



# 3.0.0 (2020-12-25)


### Bug Fixes

* **requests:** `maxRetryAfter` must be inside `retry` ([ec265d7](https://github.yandex-team.ru/search-interfaces/infratest/commit/ec265d73e12b23087b8f88a59474819e04b18ec0))
* **requests:** add ignoreRetryAfterHeader to typings ([cf7dde4](https://github.yandex-team.ru/search-interfaces/infratest/commit/cf7dde4b3cc936cf283b12c59c28e90dc8e5e447))
* **requests:** always receive the first chunk of response ([21a8b64](https://github.yandex-team.ru/search-interfaces/infratest/commit/21a8b6491c66bc9260457198a3576b70e6cdc30e))
* **requests:** do not subscribe to receive a body for successful request ([4990dc8](https://github.yandex-team.ru/search-interfaces/infratest/commit/4990dc8db03f9e06beb553c667bac06fb8e40455))
* **requests:** don't modify original status codes ([1392251](https://github.yandex-team.ru/search-interfaces/infratest/commit/1392251ec3ed956ccdb1ea7566bb3f7632ce3fe2))
* **requests:** don't read more than necessary ([32a2927](https://github.yandex-team.ru/search-interfaces/infratest/commit/32a29278eceb129e1aaf517e6a2883f2c3ec4a73))
* **requests:** fix floating tests ([3b3cb1e](https://github.yandex-team.ru/search-interfaces/infratest/commit/3b3cb1e856e0b1a94a8e32003ccf98ed56d57113))
* **requests:** now headers transform to lowercase by default ([831a32d](https://github.yandex-team.ru/search-interfaces/infratest/commit/831a32de262f21fed8cc9975c7541963dbe6be55))
* **requests:** now retriable methods is a Set ([f5a6585](https://github.yandex-team.ru/search-interfaces/infratest/commit/f5a6585afd29b120948b3bac652bd2bc6cb656b9))
* **requests:** the `gotRetry` property renamed to `retry` ([975dc2b](https://github.yandex-team.ru/search-interfaces/infratest/commit/975dc2bdb7214317dd5138a4e5d0be0ae2ba8cfa))
* **requests:** use correct property name ([624cae5](https://github.yandex-team.ru/search-interfaces/infratest/commit/624cae52c1619a8ece88d513c0a839dda9a5b597))
* **requests:** use correct structure in declaration files ([3e62b2f](https://github.yandex-team.ru/search-interfaces/infratest/commit/3e62b2f4760439c1c4fcbf274f282a395c8bc89b))


### Build System

* exclude test files from package ([89b10b4](https://github.yandex-team.ru/search-interfaces/infratest/commit/89b10b44c4051281eb3d1c18ab92d1da432345d5))


### Features

* **packages:** adds the `requests` package ([f503b2d](https://github.yandex-team.ru/search-interfaces/infratest/commit/f503b2d9c785db6ab8401ee602e59528ab6636d0))
* **requests:** ability to control max loggable length of response body ([4ac70b7](https://github.yandex-team.ru/search-interfaces/infratest/commit/4ac70b7a4a9b464a03b06b602aa376c95ef442bd))
* **requests:** add ".withRetriable404StatusCode" method ([29bf37f](https://github.yandex-team.ru/search-interfaces/infratest/commit/29bf37fa578e4b5cda93a64435cca4c697923ad4))
* **requests:** add `nonRetriableStatusCodes` property ([d892ac6](https://github.yandex-team.ru/search-interfaces/infratest/commit/d892ac6978f035e0881a950d99cb448895331876))
* **requests:** add ability to cancel retry by max total request time ([d35b758](https://github.yandex-team.ru/search-interfaces/infratest/commit/d35b7586c8424b7ea4a31539fc773dfa7bb51302))
* **requests:** add helper to allow POST retries ([86276ff](https://github.yandex-team.ru/search-interfaces/infratest/commit/86276ff4016df70c4b931f37772fb26874eabfed))
* **requests:** add information about date of the next retry ([e351db4](https://github.yandex-team.ru/search-interfaces/infratest/commit/e351db4ab058094e888f2bc7bb98d4d3a7d554a1))
* **requests:** add logging for requests & responses ([c38873f](https://github.yandex-team.ru/search-interfaces/infratest/commit/c38873fa4d3f5a01e21d162588e540619f3ff113))
* **requests:** add retry.ignoreRetryAfterHeader ([ff414a9](https://github.yandex-team.ru/search-interfaces/infratest/commit/ff414a962198500401b822c198356953148d953a))
* **requests:** add rich retry logic ([a4d45ad](https://github.yandex-team.ru/search-interfaces/infratest/commit/a4d45adb440267510de36dfa9bffc4468cf6a5d9))
* **requests:** add types for options ([c5fe746](https://github.yandex-team.ru/search-interfaces/infratest/commit/c5fe746bcfb8e648c11d5866b92abd7b15864a04))
* **requests:** don't change user headers (X-Request-ID) ([06f6820](https://github.yandex-team.ru/search-interfaces/infratest/commit/06f68208d5a87eb65740b535e883bb7e5e1c8924))
* **requests:** export usable constants ([5adb6ca](https://github.yandex-team.ru/search-interfaces/infratest/commit/5adb6caeb4f16a017bbada64b283133c78982541))
* **requests:** increase allowed body log length ([b06b14b](https://github.yandex-team.ru/search-interfaces/infratest/commit/b06b14bb2ae224938a54f40e215145788a876277))
* **requests:** non retriable 404 status ([520c96e](https://github.yandex-team.ru/search-interfaces/infratest/commit/520c96ec20357ceaaaa3a90184c4aeea23d422e1))
* **requests:** setup base retries of requests ([8dc0325](https://github.yandex-team.ru/search-interfaces/infratest/commit/8dc03256003d006c89d910f2388f3eb1f3c7f6c9))
* **requests:** update `got` package to the latest version ([ddb9420](https://github.yandex-team.ru/search-interfaces/infratest/commit/ddb9420612b2d432c59b7f7b6dfa6ef2cba7ecde))
* **requests:** update got version ([6bd0155](https://github.yandex-team.ru/search-interfaces/infratest/commit/6bd015513face7ffd360834dc3a453b1e7838f05))
* **requests:** use branded UA for requests ([c132569](https://github.yandex-team.ru/search-interfaces/infratest/commit/c132569629b0c82a910e48ac256916036b2e8be3))
* **requests:** use same ID for request and its retries ([ff63482](https://github.yandex-team.ru/search-interfaces/infratest/commit/ff634826e82e6c529a78d70f7b18ec46af22c3c2))


### BREAKING CHANGES

* **requests:** нужно выпутсить мажор с новой функциональностью.
* Первая мажорная версия пакета.
