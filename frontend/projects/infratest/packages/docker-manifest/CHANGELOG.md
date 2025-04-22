# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [2.0.49](https://github.yandex-team.ru/search-interfaces/infratest.gi/compare/@yandex-int/si.ci.docker-manifest@2.0.49...@yandex-int/si.ci.docker-manifest@2.0.49) (2021-03-13)



## 2.0.49 (2021-03-12)



## 2.0.48 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 2.0.47 (2021-03-12)



## 2.0.46 (2021-03-10)



## 2.0.45 (2021-03-10)



## [2.0.44](https://github.yandex-team.ru/search-interfaces/infratest.gi/compare/d330f6eeaac74032e16be3850e180c8c03230c6c...@yandex-int/si.ci.docker-manifest@2.0.44) (2021-03-10)


### Bug Fixes

* **docker-manifest:** исправить отправку accept-заголовка ([90a4a12](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/90a4a12757e9c2f69f25b0f0360fa62c6f3fe916))
* перевёл все секреты, уже использующие env-utils ([89c5298](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/89c5298e97327cc01f664b138e18fac83c25bd86))
* **docker-manifest:** lowercase для HTTP-заголовков ([44b0406](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/44b04066af2cd891adcc21c988c39dff2bbd544d))
* **docker-manifest:** update docker-reference to v1.0.0 ([5050d2c](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/5050d2ce3614cece98b2ce9f9c731ddc12b4e5ae))
* **docker-manifest:** не падать без env-переменной ([d875358](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/d875358c1d3bb0e4629962a8d779bf745baf36af)), closes [/github.yandex-team.ru/qloud/qloud-api/commit/3cbd84cc256c69c1143e4d165a63000f002b04db#diff-6d186b954a58d5bb740f73d84fe39073R7](https://github.yandex-team.ru/search-interfaces/infratest.gi/issues/diff-6d186b954a58d5bb740f73d84fe39073R7)


### Code Refactoring

* **docker-manifest:** rename method ([4f1dd9b](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/4f1dd9b775aa2eabf26d82b1319d702f9d02c6ab))


### Features

* добавил пакет docker-manifest ([d330f6e](https://github.yandex-team.ru/search-interfaces/infratest.gi/commit/d330f6eeaac74032e16be3850e180c8c03230c6c))


### BREAKING CHANGES

* **docker-manifest:** rename method `getImageManifest` to `fetchImageManifest`

`fetch` больше подразумевает длительный асинхронный процесс, чем `get`.
