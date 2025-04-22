# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

# 4.0.0 (2021-03-17)


### Bug Fixes

* **ab-experiments:** ability to perform for search with multiple experiments ([137f556](https://github.yandex-team.ru/search-interfaces/infratest/commit/137f5564b9b01c4a346a2383b2a02d812d19fd06))
* **ab-experiments:** fix method signature in declaration file ([390981a](https://github.yandex-team.ru/search-interfaces/infratest/commit/390981af3fa7380388d3912c77cd438f1f35add1))
* **ab-experiments:** send requests sequentially ([3fa2ef7](https://github.yandex-team.ru/search-interfaces/infratest/commit/3fa2ef7cf9a9fc47ba2c72b8d4d62a6b6ff44ddd))
* **ab-experiments:** show params in logs correctly ([7beb445](https://github.yandex-team.ru/search-interfaces/infratest/commit/7beb4453367a2d74cb21e98953111a541bd0a0aa))
* **ab-experiments:** Возвращать body ([2c2186a](https://github.yandex-team.ru/search-interfaces/infratest/commit/2c2186a67db7c6b905ea8217db9d739730dd6d9a))
* **ab-experiments:** искать только активные testid ([ea8d4ab](https://github.yandex-team.ru/search-interfaces/infratest/commit/ea8d4abeece1a7d2a8aec718de92e9f920b4d0fd))
* **ab-experiments:** нет ошибки для запроса ([a73f343](https://github.yandex-team.ru/search-interfaces/infratest/commit/a73f343600dccececf8c6c0f0e36c297ac2d5d11))
* **testid-cli:** do not throw an exception calling command with help ([a0fe27b](https://github.yandex-team.ru/search-interfaces/infratest/commit/a0fe27b22548db11949dd61a11ad9114cba065b2))
* **testid-cli:** fetch flags only for one author ([b7f40a9](https://github.yandex-team.ru/search-interfaces/infratest/commit/b7f40a9c53711dfd2d4753723feadbce2289629a))
* перевёл все секреты, уже использующие env-utils ([542957c](https://github.yandex-team.ru/search-interfaces/infratest/commit/542957c7b83449991e10f9c20a68fd79becb033a))
* **testid-cli:** лишние testid для rearr-флагов ([a5e7037](https://github.yandex-team.ru/search-interfaces/infratest/commit/a5e7037260d9aaa1ee76e064f847930c5bec7fe2))
* **testid-cli:** проставлять zero_testing_application тег для testid ([5820914](https://github.yandex-team.ru/search-interfaces/infratest/commit/5820914a854d7792f71fa4f66c97660fdb42abab)), closes [/st.yandex-team.ru/USEREXP-4910#1508505257000](https://github.yandex-team.ru/search-interfaces/infratest/issues/1508505257000)


### Features

* **ab-experiment:** add getExperimentTask method ([153cca1](https://github.yandex-team.ru/search-interfaces/infratest/commit/153cca15e45cca46068009e59ae7a19b99fbf8f6))
* **ab-experiments:** ability to apply custom paramteres to request ([8be429d](https://github.yandex-team.ru/search-interfaces/infratest/commit/8be429d72f750683d93bec60480b2a2b4d4064eb))
* **ab-experiments:** ability to mark flag as removed from code ([2f239b9](https://github.yandex-team.ru/search-interfaces/infratest/commit/2f239b99d45d0b0be53fe772fae9ea178663557c))
* **ab-experiments:** add activateExperiment method ([4b8506a](https://github.yandex-team.ru/search-interfaces/infratest/commit/4b8506a65ab145ec3cd0759778173199579359ba))
* **ab-experiments:** add handler for depracating flags ([24fd9ce](https://github.yandex-team.ru/search-interfaces/infratest/commit/24fd9ce7661cc64ab3b50034e6bd312f8af73d2a))
* **ab-experiments:** add source for flag deprecation ([0903896](https://github.yandex-team.ru/search-interfaces/infratest/commit/0903896e6548729ed17a39e00bec97aee4624857))
* **ab-experiments:** add the "searchTestIds" method ([ce018d4](https://github.yandex-team.ru/search-interfaces/infratest/commit/ce018d4e56053d85acf59e2e7398061b360a3358))
* **ab-experiments:** add updateExperiment method ([2edb5a1](https://github.yandex-team.ru/search-interfaces/infratest/commit/2edb5a1e80f0a6b4c0d21e0f38918bdaa65b3414))
* **ab-experiments:** change ab endpoint for flags operations ([ea04238](https://github.yandex-team.ru/search-interfaces/infratest/commit/ea04238d01e8a743861f5cd8513327f0e254fea9))
* **ab-experiments:** get testid's by chunks ([ca461d7](https://github.yandex-team.ru/search-interfaces/infratest/commit/ca461d7440a46d16038329f3bda377afb281288a))
* **ab-experiments:** handle API to fetch issue related testids ([1e29a0b](https://github.yandex-team.ru/search-interfaces/infratest/commit/1e29a0b8183bca5a50caab5bb2770ef22f75881a))
* **ab-experiments:** remove 'removeFlagFromStorage' method ([3b3069a](https://github.yandex-team.ru/search-interfaces/infratest/commit/3b3069a6dbfe8d32ef0bdf88a6dc1afa7b784fa7))
* **ab-experiments:** searchFullTestIds method ([8722f99](https://github.yandex-team.ru/search-interfaces/infratest/commit/8722f99c3f6fc16e865c2b99eeccad184da86fe9))
* **ab-experiments:** testid by tag arbitary query ([1e7f1ba](https://github.yandex-team.ru/search-interfaces/infratest/commit/1e7f1ba6e9327b127eb2eb0839e4122f5b2b9170))
* **ab-experiments:** uploadFlagAtStorage ([37bbe59](https://github.yandex-team.ru/search-interfaces/infratest/commit/37bbe5960ad38c2013beeca24ea23110a69ae97b))
* **ab-experiments:** use API v1 in 'getAllFlagsFromStorage' method ([6ebf6be](https://github.yandex-team.ru/search-interfaces/infratest/commit/6ebf6be2ba31855a7fb32e1848c92a845a617355))
* **ab-experiments:** use TestIdTag instead of string ([4faeae4](https://github.yandex-team.ru/search-interfaces/infratest/commit/4faeae4b6738338b7715626369e3b554f37929e8))
* **ab-experiments:** Возможность создавать эксперименты (test-id) ([c9b8d98](https://github.yandex-team.ru/search-interfaces/infratest/commit/c9b8d98239ed48d77ac433834a9de6f8e4f5a806))
* **ab-experiments:** возможность указать конфиг в /activity/current ([8572052](https://github.yandex-team.ru/search-interfaces/infratest/commit/857205232072a62c88d439b4948799d309943e80))
* **ab-experiments:** работа со стораджем флагов ([ce61f20](https://github.yandex-team.ru/search-interfaces/infratest/commit/ce61f20aa760b389f69f294df127bb9c9dd3fb52))
* **ab-experiments:** ручка для поиска test-id по флагам ([f8e10d2](https://github.yandex-team.ru/search-interfaces/infratest/commit/f8e10d2e357935e1b40d650ec6dec7d384c30472))
* **ab-experiments:** ручки для публикации testid ([684df17](https://github.yandex-team.ru/search-interfaces/infratest/commit/684df17051902d82f3890669a805eeb949d06503))
* **testid-cli:** создание и публикация testid ([49ceaed](https://github.yandex-team.ru/search-interfaces/infratest/commit/49ceaed65716b09016dfd6a16d8848cb8700f83e))


### BREAKING CHANGES

* **ab-experiments:** метод `getExperimentsByTag` вторым аргументом теперь
принимает произвольные параметры, которые будут переданы в query запроса
* **ab-experiments:** перевёл на новое апи ручки для работы с флагами:
- get
- create
- update
- deprecate





## [3.6.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.6.3...@yandex-int/si.ci.ab-experiments@3.6.4) (2021-01-26)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.6.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.6.2...@yandex-int/si.ci.ab-experiments@3.6.3) (2021-01-11)


### Bug Fixes

* **ab-experiments:** ability to perform for search with multiple experiments ([8254773](https://github.yandex-team.ru/search-interfaces/ci/commit/8254773))





## [3.6.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.6.1...@yandex-int/si.ci.ab-experiments@3.6.2) (2020-11-16)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.6.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.6.0...@yandex-int/si.ci.ab-experiments@3.6.1) (2020-10-30)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





# [3.6.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.5.5...@yandex-int/si.ci.ab-experiments@3.6.0) (2020-10-20)


### Features

* **ab-experiments:** get testid's by chunks ([2f7d21a](https://github.yandex-team.ru/search-interfaces/ci/commit/2f7d21a))





## [3.5.5](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.5.4...@yandex-int/si.ci.ab-experiments@3.5.5) (2020-09-30)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.5.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.5.3...@yandex-int/si.ci.ab-experiments@3.5.4) (2020-09-24)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.5.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.5.2...@yandex-int/si.ci.ab-experiments@3.5.3) (2020-09-17)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.5.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.5.1...@yandex-int/si.ci.ab-experiments@3.5.2) (2020-08-06)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.5.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.5.0...@yandex-int/si.ci.ab-experiments@3.5.1) (2020-07-29)


### Bug Fixes

* **ab-experiments:** fix method signature in declaration file ([1f24355](https://github.yandex-team.ru/search-interfaces/ci/commit/1f24355))





# [3.5.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.4.0...@yandex-int/si.ci.ab-experiments@3.5.0) (2020-07-29)


### Features

* **ab-experiments:** ability to apply custom paramteres to request ([f03cedf](https://github.yandex-team.ru/search-interfaces/ci/commit/f03cedf))





# [3.4.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.3.0...@yandex-int/si.ci.ab-experiments@3.4.0) (2020-06-10)


### Features

* **ab-experiments:** add activateExperiment method ([2c643a1](https://github.yandex-team.ru/search-interfaces/ci/commit/2c643a1))
* **ab-experiments:** add updateExperiment method ([dc8304a](https://github.yandex-team.ru/search-interfaces/ci/commit/dc8304a))





# [3.3.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.2.0...@yandex-int/si.ci.ab-experiments@3.3.0) (2020-06-04)


### Features

* **ab-experiments:** searchFullTestIds method ([b4ae468](https://github.yandex-team.ru/search-interfaces/ci/commit/b4ae468))





# [3.2.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.1.3...@yandex-int/si.ci.ab-experiments@3.2.0) (2020-03-06)


### Features

* **ab-experiments:** use TestIdTag instead of string ([4ede95d](https://github.yandex-team.ru/search-interfaces/ci/commit/4ede95d))





## [3.1.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.1.2...@yandex-int/si.ci.ab-experiments@3.1.3) (2020-02-20)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.1.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.1.1...@yandex-int/si.ci.ab-experiments@3.1.2) (2020-02-12)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [3.1.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.1.0...@yandex-int/si.ci.ab-experiments@3.1.1) (2020-01-29)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





# [3.1.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@3.0.0...@yandex-int/si.ci.ab-experiments@3.1.0) (2020-01-20)


### Features

* **ab-experiments:** ability to mark flag as removed from code ([49f8bd6](https://github.yandex-team.ru/search-interfaces/ci/commit/49f8bd6))





# [3.0.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.6...@yandex-int/si.ci.ab-experiments@3.0.0) (2019-11-19)


### Features

* **ab-experiments:** testid by tag arbitary query ([bdec812](https://github.yandex-team.ru/search-interfaces/ci/commit/bdec812))


### BREAKING CHANGES

* **ab-experiments:** метод `getExperimentsByTag` вторым аргументом теперь
принимает произвольные параметры, которые будут переданы в query запроса





## [2.1.6](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.5...@yandex-int/si.ci.ab-experiments@2.1.6) (2019-10-21)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.1.5](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.4...@yandex-int/si.ci.ab-experiments@2.1.5) (2019-10-18)


### Bug Fixes

* **ab-experiments:** send requests sequentially ([916bfc5](https://github.yandex-team.ru/search-interfaces/ci/commit/916bfc5))
* **testid-cli:** fetch flags only for one author ([038c7c1](https://github.yandex-team.ru/search-interfaces/ci/commit/038c7c1))





## [2.1.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.3...@yandex-int/si.ci.ab-experiments@2.1.4) (2019-09-18)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.1.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.2...@yandex-int/si.ci.ab-experiments@2.1.3) (2019-09-18)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.1.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.1...@yandex-int/si.ci.ab-experiments@2.1.2) (2019-09-17)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.1.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.1.0...@yandex-int/si.ci.ab-experiments@2.1.1) (2019-09-13)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





# [2.1.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.0.5...@yandex-int/si.ci.ab-experiments@2.1.0) (2019-08-27)


### Features

* **ab-experiments:** add source for flag deprecation ([9183ca9](https://github.yandex-team.ru/search-interfaces/ci/commit/9183ca9))





## [2.0.5](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.0.4...@yandex-int/si.ci.ab-experiments@2.0.5) (2019-08-07)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.0.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.0.3...@yandex-int/si.ci.ab-experiments@2.0.4) (2019-08-07)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.0.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.0.2...@yandex-int/si.ci.ab-experiments@2.0.3) (2019-08-07)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.0.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.0.1...@yandex-int/si.ci.ab-experiments@2.0.2) (2019-08-07)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [2.0.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@2.0.0...@yandex-int/si.ci.ab-experiments@2.0.1) (2019-08-07)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





## [1.11.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.11.0...@yandex-int/si.ci.ab-experiments@1.11.1) (2019-05-29)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





# [1.11.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.10.0...@yandex-int/si.ci.ab-experiments@1.11.0) (2019-04-25)


### Features

* **ab-experiment:** add getExperimentTask method ([9f2bb1a](https://github.yandex-team.ru/search-interfaces/ci/commit/9f2bb1a))





<a name="1.10.0"></a>
# [1.10.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.9.1...@yandex-int/si.ci.ab-experiments@1.10.0) (2019-02-20)


### Features

* **ab-experiments:** add the "searchTestIds" method ([6e979a6](https://github.yandex-team.ru/search-interfaces/ci/commit/6e979a6))





<a name="1.9.1"></a>
## [1.9.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.9.0...@yandex-int/si.ci.ab-experiments@1.9.1) (2019-01-17)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.9.0"></a>
# [1.9.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.16...@yandex-int/si.ci.ab-experiments@1.9.0) (2018-11-29)


### Features

* **ab-experiments:** handle API to fetch issue related testids ([0e9a355](https://github.yandex-team.ru/search-interfaces/ci/commit/0e9a355))





<a name="1.8.16"></a>
## [1.8.16](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.15...@yandex-int/si.ci.ab-experiments@1.8.16) (2018-11-28)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.15"></a>
## [1.8.15](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.14...@yandex-int/si.ci.ab-experiments@1.8.15) (2018-11-22)


### Bug Fixes

* **testid-cli:** do not throw an exception calling command with help ([02b2a8b](https://github.yandex-team.ru/search-interfaces/ci/commit/02b2a8b))





<a name="1.8.14"></a>
## [1.8.14](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.13...@yandex-int/si.ci.ab-experiments@1.8.14) (2018-11-08)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.13"></a>
## [1.8.13](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.12...@yandex-int/si.ci.ab-experiments@1.8.13) (2018-11-07)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.12"></a>
## [1.8.12](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.11...@yandex-int/si.ci.ab-experiments@1.8.12) (2018-11-06)


### Bug Fixes

* **ab-experiments:** show params in logs correctly ([6711a96](https://github.yandex-team.ru/search-interfaces/ci/commit/6711a96))





<a name="1.8.11"></a>
## [1.8.11](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.10...@yandex-int/si.ci.ab-experiments@1.8.11) (2018-10-31)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.10"></a>
## [1.8.10](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.9...@yandex-int/si.ci.ab-experiments@1.8.10) (2018-10-24)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.9"></a>
## [1.8.9](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.8...@yandex-int/si.ci.ab-experiments@1.8.9) (2018-10-23)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.8"></a>
## [1.8.8](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.7...@yandex-int/si.ci.ab-experiments@1.8.8) (2018-10-22)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.7"></a>
## [1.8.7](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.6...@yandex-int/si.ci.ab-experiments@1.8.7) (2018-10-22)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.6"></a>
## [1.8.6](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.5...@yandex-int/si.ci.ab-experiments@1.8.6) (2018-10-18)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.5"></a>
## [1.8.5](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.4...@yandex-int/si.ci.ab-experiments@1.8.5) (2018-10-17)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.4"></a>
## [1.8.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.3...@yandex-int/si.ci.ab-experiments@1.8.4) (2018-10-15)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.3"></a>
## [1.8.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.2...@yandex-int/si.ci.ab-experiments@1.8.3) (2018-10-12)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.2"></a>
## [1.8.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.1...@yandex-int/si.ci.ab-experiments@1.8.2) (2018-10-12)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.1"></a>
## [1.8.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.8.0...@yandex-int/si.ci.ab-experiments@1.8.1) (2018-10-12)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.8.0"></a>
# [1.8.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.7.5...@yandex-int/si.ci.ab-experiments@1.8.0) (2018-10-10)


### Features

* **ab-experiments:** add handler for depracating flags ([9aee662](https://github.yandex-team.ru/search-interfaces/ci/commit/9aee662))





<a name="1.7.5"></a>
## [1.7.5](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.7.4...@yandex-int/si.ci.ab-experiments@1.7.5) (2018-10-08)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.7.4"></a>
## [1.7.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.7.3...@yandex-int/si.ci.ab-experiments@1.7.4) (2018-09-12)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.7.3"></a>
## [1.7.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.7.2...@yandex-int/si.ci.ab-experiments@1.7.3) (2018-08-31)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.7.2"></a>
## [1.7.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.7.1...@yandex-int/si.ci.ab-experiments@1.7.2) (2018-08-27)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.7.1"></a>
## [1.7.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.7.0...@yandex-int/si.ci.ab-experiments@1.7.1) (2018-08-24)

**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments





<a name="1.7.0"></a>
# [1.7.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.6.0...@yandex-int/si.ci.ab-experiments@1.7.0) (2018-07-23)


### Bug Fixes

* **ab-experiments:** нет ошибки для запроса ([f8b0ec7](https://github.yandex-team.ru/search-interfaces/ci/commit/f8b0ec7))


### Features

* **ab-experiments:** uploadFlagAtStorage ([15bdfac](https://github.yandex-team.ru/search-interfaces/ci/commit/15bdfac))




<a name="1.6.0"></a>
# [1.6.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.5.4...@yandex-int/si.ci.ab-experiments@1.6.0) (2018-07-16)


### Features

* **ab-experiments:** работа со стораджем флагов ([fb40e90](https://github.yandex-team.ru/search-interfaces/ci/commit/fb40e90))




<a name="1.5.4"></a>
## [1.5.4](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.5.3...@yandex-int/si.ci.ab-experiments@1.5.4) (2018-05-30)


### Bug Fixes

* перевёл все секреты, уже использующие env-utils ([ca4714c](https://github.yandex-team.ru/search-interfaces/ci/commit/ca4714c))




<a name="1.5.3"></a>
## [1.5.3](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.5.2...@yandex-int/si.ci.ab-experiments@1.5.3) (2018-05-24)




**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments

<a name="1.5.2"></a>
## [1.5.2](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.5.1...@yandex-int/si.ci.ab-experiments@1.5.2) (2018-04-05)


### Bug Fixes

* **testid-cli:** лишние testid для rearr-флагов ([510e2db](https://github.yandex-team.ru/search-interfaces/ci/commit/510e2db))




<a name="1.5.1"></a>
## [1.5.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.5.0...@yandex-int/si.ci.ab-experiments@1.5.1) (2018-04-02)


### Bug Fixes

* **ab-experiments:** искать только активные testid ([e5bea73](https://github.yandex-team.ru/search-interfaces/ci/commit/e5bea73))




<a name="1.5.0"></a>
# [1.5.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.4.0...@yandex-int/si.ci.ab-experiments@1.5.0) (2018-03-30)


### Features

* **ab-experiments:** возможность указать конфиг в /activity/current ([21198f6](https://github.yandex-team.ru/search-interfaces/ci/commit/21198f6))




<a name="1.4.0"></a>
# [1.4.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.3.0...@yandex-int/si.ci.ab-experiments@1.4.0) (2018-03-30)


### Bug Fixes

* **testid-cli:** проставлять zero_testing_application тег для testid ([412e3e5](https://github.yandex-team.ru/search-interfaces/ci/commit/412e3e5)), closes [/st.yandex-team.ru/USEREXP-4910#1508505257000](https://github.yandex-team.ru//st.yandex-team.ru/USEREXP-4910/issues/1508505257000)


### Features

* **ab-experiments:** ручки для публикации testid ([ba5ca75](https://github.yandex-team.ru/search-interfaces/ci/commit/ba5ca75))




<a name="1.3.0"></a>
# [1.3.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.2.0...@yandex-int/si.ci.ab-experiments@1.3.0) (2018-03-28)


### Features

* **ab-experiments:** ручка для поиска test-id по флагам ([9fd89d1](https://github.yandex-team.ru/search-interfaces/ci/commit/9fd89d1))
* **testid-cli:** создание и публикация testid ([bf77f05](https://github.yandex-team.ru/search-interfaces/ci/commit/bf77f05))




<a name="1.2.0"></a>
# 1.2.0 (2018-02-06)


### Bug Fixes

* **ab-experiments:** Возвращать body ([791b2f3](https://github.yandex-team.ru/search-interfaces/ci/commit/791b2f3))


### Features

* **ab-experiments:** Возможность создавать эксперименты (test-id) ([6df3eee](https://github.yandex-team.ru/search-interfaces/ci/commit/6df3eee))




<a name="1.1.1"></a>
## [1.1.1](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.1.0...@yandex-int/si.ci.ab-experiments@1.1.1) (2018-02-02)


### Bug Fixes

* **ab-experiments:** Возвращать body ([791b2f3](https://github.yandex-team.ru/search-interfaces/ci/commit/791b2f3))




<a name="1.1.0"></a>
# [1.1.0](https://github.yandex-team.ru/search-interfaces/ci/compare/@yandex-int/si.ci.ab-experiments@1.0.0...@yandex-int/si.ci.ab-experiments@1.1.0) (2018-02-02)


### Features

* **ab-experiments:** Возможность создавать эксперименты (test-id) ([6df3eee](https://github.yandex-team.ru/search-interfaces/ci/commit/6df3eee))




<a name="1.0.0"></a>
# 1.0.0 (2018-01-31)




**Note:** Version bump only for package @yandex-int/si.ci.ab-experiments
