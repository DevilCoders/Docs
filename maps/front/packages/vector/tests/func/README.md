# Autotests for Vector Map
Tests compare two versions of maps using [Hermione](https://github.com/gemini-testing/hermione/).

By default, tests are run in [Selenium-grid](https://selenium.yandex-team.ru/#quota/selenium).

Checklist for vector map's testing [here](https://github.yandex-team.ru/maps/vector/blob/dev/doc/test/checklist.md).

About design's testing [here](https://github.yandex-team.ru/maps/vector/blob/dev/doc/test/design.md).

About customization's testing [here](https://github.yandex-team.ru/maps/vector/blob/dev/doc/test/customization.md).

## About configuring the environment
 <details>
      <summary>More detailed</summary>

### Windows

1. Установить эмулятор консоли, либо воспользоваться консолью Win с помощью команд WIN + R + Enter.
2. Клонировать репозиторий: 
    - создать директорию на ПК в которую поместите проект;
    - открыть консоль, с помощью команды cd прописать путь в директорию/папку; 
    - ввести команду git clone https://github.yandex-team.ru/maps/vector.git и загрузить репозиторий в папку.
3. Установить [Node JS](https://nodejs.org/en/download/).
4. Установить подсистему Linux в Windows 10 - [руководство по установке](https://docs.microsoft.com/ru-ru/windows/wsl/install-win10). Можно пройти в Microsoft Store и установить оттуда Ubuntu 18.04 LTS или другой дистрибутив Linux.
5. После установки открыть терминал Ubuntu. В терминале последовательно ввести команды:
`sudo apt update`
`sudo apt install make nodejs npm`
6. C помощью команды `cd` пройти в директорию проекта `vector/tests/funс`, в которой ввести команду `sudo apt make install` - устанавливаем пакеты зависимостей проекта. 
7. После установки всех пакетов, выполните перезагрузку.
8. Заходим в консоль, пишем в консоли команду wsl, после ввода данной команды, консоль должна входить в подсистему Ubuntu.
    - после двоеточия должен стоять путь `/mnt/c`, это значит что мы можем строить дальнейший путь к файлам полученным с репозитория и запускать сборку тестов. Путь имеет вид `/mnt/c`, поскольку вы проходите к файлам из подсистемы Ubuntu установленной на ПК. Путь к файлам клонированного репозитория: `.../Созданная_папка/vector`, где многоточие путь от диска;
    - если в консоли получить искомый путь не вышло, попробуйте зайти в терминал подсистемы Ubuntu и самостоятельно ввести комбинацию `cd /mnt/c/.../Созданная_папка/vector`, маленькая `с` в данном случае - это диск С в Windows.
9. После выполнения шагов пройдите по пути `vector/tests/funс` используя подсистему `wsl` и выполните команду `make test-map-design`.
    - при наличии сообщений об ошибках внимательно изучите их, чтобы выполнить необходимые шаги по устранению неполадок.

### Mac/Linux

1. Выполняйте шаги **№№ 2, 3, 5, 6, 7**(не устанавливая подсистему WSL) инструкции Windows используя терминал.
    </details>

## Getting started
```
cd tests/func
```

Install the packages
```
make install
```

## Run tests
`Reference` is first running of tests for getting reference screenshots.
`Actual` is second with vector version under development.

----

Environment: testing, reference: raster map
```
make test
```

Environment: production, reference: raster map
```
make test-prod
```

Environment: testing with production tiles, reference: raster map
```
make test-prod-tiles
```

Reference: production vector map, actual: testing vector map with production tiles
```
make test-vector-prod-testing
```
[Sandbox vector-testing with prod tiles](https://sandbox.yandex-team.ru/scheduler/17982/view)

[Sandbox prod – datatestig](https://sandbox.yandex-team.ru/scheduler/18009/view)

Launch performance test for getting average time of rendering vector map on start
```
make test-get-start-time
```
## Run map design tests
```
make test-map-design
```
[Sandbox Vector](https://sandbox.yandex-team.ru/scheduler/17518/view)

[Sandbox Raster](https://sandbox.yandex-team.ru/scheduler/17914/view)

[Tiles' hosts](./hosts/design.json)

[Cases](./test-design/cases.js)

### How to add new set/case to [list](./test-design/cases.js)
```
{
    <set name>: [
        {name: <case name>, center: <map center>, zmin: <zoom from>, zmax: <zoom to>}
    ]
}
```


## Environment variables

Variable                  | Description
------------------------- | -------------
`ARGS`                    | Options for override hermione configurations. For example, ```make test ARGS='--reporter plain'```
`API_VERSION`             | Default API version is `2.1.71`. This variable will override it. Example, ```make test API_VERSION=2.1.72```
`API_VERSION_REFERENCE`   | Api version for references maps. Default value is `API_VERSION`
`API_VERSION_ACTUAL`      | Api version for compared maps. Default value is `API_VERSION`
`ENVIRONMENT_REFERENCE`   | Valid values are `PRODUCTION`, `TESTING`, `TESTING_OVERRIDDEN_HOSTS`
`ENVIRONMENT_ACTUAL`      | Valid values are `PRODUCTION`, `TESTING`, `TESTING_OVERRIDDEN_HOSTS`


## Report
After passing the tests you can see a link to the report in console
`Your HTML report is here: file://...`

### Meta information
Each test has meta information in report

Meta key                  | Description
------------------------- | -------------
`center`                  | Map center
`zoom`                    | Map zoom
`maps`                    | Link to https://l7test.yandex.ru/maps with map's options
`apiReference`            | Link to API of reference maps
`apiActual`               | Link to API of actual maps
`envReference`            | Environment of reference maps. `PRODUCTION`, `TESTING`, `TESTING_OVERRIDDEN_HOSTS`
`envActual`               | Environment of actual maps. `PRODUCTION`, `TESTING`, `TESTING_OVERRIDDEN_HOSTS`
`file`                    | Filename of test


## How to retry specific tests

1. By using reporter gui

```
make [last-running-test-command] TYPE=ACTUAL ARGS=qui
```
Example,
```
make test-prod-tiles TYPE=ACTUAL ARGS=qui
```

2. By using `.only`

[hermione.only](https://github.com/gemini-testing/hermione#only)
