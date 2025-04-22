# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

## [4.2.31](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.qloud-api@4.2.31...@yandex-int/si.ci.qloud-api@4.2.31) (2021-03-13)



## 4.2.31 (2021-03-12)



## 4.2.30 (2021-03-12)


### Bug Fixes

* satisfy package-checker ([d319091](https://github.yandex-team.ru/search-interfaces/infratest/commit/d319091dbb014ad157b3b3cf9de412910b3191ba))



## 4.2.29 (2021-03-12)



## 4.2.28 (2021-03-10)



## 4.2.27 (2021-03-10)



## 4.2.26 (2021-03-09)



## 4.2.25 (2021-02-09)



## [4.2.24](https://github.yandex-team.ru/search-interfaces/infratest/compare/@yandex-int/si.ci.qloud-api@4.2.23...@yandex-int/si.ci.qloud-api@4.2.24) (2021-01-30)



## [4.2.23](https://github.yandex-team.ru/search-interfaces/infratest/compare/b38dde31b1724d0dfd2b77195a3b17aaa246ce1c...@yandex-int/si.ci.qloud-api@4.2.23) (2021-01-30)


### Bug Fixes

* **debug:** change namespace ([940b75b](https://github.yandex-team.ru/search-interfaces/infratest/commit/940b75b322a405a60e2ae195ce6eae10686351c4))
* **fei-13943:** причесать зависимости в пакетах ([5942302](https://github.yandex-team.ru/search-interfaces/infratest/commit/5942302e3afd7bc2131083c3f32cb1f23b1ddf4d))
* **qloud-api:** brought the cas package ([074ef58](https://github.yandex-team.ru/search-interfaces/infratest/commit/074ef58d9176fdd4b145ad5665971d7b8201cb4f))
* **qloud-api:** debug after fetch docker hash ([992e2cc](https://github.yandex-team.ru/search-interfaces/infratest/commit/992e2cc05086d59514fd941ed4894910e9e16559))
* **qloud-api:** debug properties for deployDockerComponent ([4d49496](https://github.yandex-team.ru/search-interfaces/infratest/commit/4d4949640cc12352014ad4c038142a72918328d6))
* **qloud-api:** remove "retryCount" from "getStableEnvironment" ([460f133](https://github.yandex-team.ru/search-interfaces/infratest/commit/460f1333cbf12db99e7c1b6a0a5193d7187b7494))
* **qloud-api:** repository is not required for deployDockerComponent ([06ca18f](https://github.yandex-team.ru/search-interfaces/infratest/commit/06ca18fa001ab9a754c1015b541796dc7db1fa78))
* **qloud-api:** should use hash from docker manifest ([3c24dfd](https://github.yandex-team.ru/search-interfaces/infratest/commit/3c24dfd297cd3563916698cfce8b33b698c18e2f))
* **qloud-api:** зафиксировать версии зависимостей ([1ddb08b](https://github.yandex-team.ru/search-interfaces/infratest/commit/1ddb08b1b38f9d40ddb3eafa0639d77155400e9e))
* **qloud-api:** исправил jsdoc для deployDockerComponent ([e592c23](https://github.yandex-team.ru/search-interfaces/infratest/commit/e592c23365f90fe1630402be92c8e11491fd8500))
* **qloud-api:** обновить package.json ([14b7883](https://github.yandex-team.ru/search-interfaces/infratest/commit/14b7883e3b79f01d9148a1616b134c6f6a39ff38))
* **qloud-api:** переименовал пакет ([ffabced](https://github.yandex-team.ru/search-interfaces/infratest/commit/ffabced7043200fe4b0fefe31fb1037f1fb325d9))
* **readme:** исправил ссылку на репо ([b38dde3](https://github.yandex-team.ru/search-interfaces/infratest/commit/b38dde31b1724d0dfd2b77195a3b17aaa246ce1c))


### Code Refactoring

* **qloud-api:** actualize aioud-api ([efe27be](https://github.yandex-team.ru/search-interfaces/infratest/commit/efe27bea23cf5bcbba5c9cc5d0d58063c7fc1b3b))


### Features

* **qloud-api:** add new method "getEnvironmentSatatus" ([31ae261](https://github.yandex-team.ru/search-interfaces/infratest/commit/31ae26177122daff704d75e4f7e862f50062ba37))
* **qloud-api:** log requests ([91dcea4](https://github.yandex-team.ru/search-interfaces/infratest/commit/91dcea48fdb3acf54e9ff7046d05472a39f86877))
* deployDockerComponent ([86a54da](https://github.yandex-team.ru/search-interfaces/infratest/commit/86a54da5e51cb4cf785b24d3739e2a2dbbc23de3))


### Performance Improvements

* **qloud-api:** should not fetch docker manifest if hash is specified ([8bba19f](https://github.yandex-team.ru/search-interfaces/infratest/commit/8bba19f86527fd32cffbe25bfbc982ee3d8dc094))


### BREAKING CHANGES

* **qloud-api:** Постарался актуализировать qloud-api. Есть 2 документации: актуальная - https://wiki.yandex-team.ru/qloud/doc/api/, устаревшая - https://wiki.yandex-team.ru/qe/qloud-api/. Правда такая, что актуальное API в коде, как ни странно. Поэтому методы, которых уже нет в коде я удалил, на остальные, которых нет в новой документации, но они еще "живы", я сделал короткие ссылки на код (нужно для того, что бы при следующей итерации актуализации удалить несуществующие методы).
