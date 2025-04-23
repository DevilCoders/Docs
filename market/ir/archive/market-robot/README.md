В данном репозитории содержатся два компонента:

mbo-robot-ui [![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Ir_MboRobotUiDeploy/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Ir_MboRobotUiDeploy)
Интерфейс робота Маркета

market-robot-tms [![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Ir_MarketRobotTmsDeploy/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Ir_MarketRobotTmsDeploy)
Робот Маркета (распределенная система запуска задач робота)

market-robot-core
Общий модуль между mbo-robot-ui и market-robot-tms.
Не публикуется и все от него должны зависеть по исходникам.


Сборка и выкладка компонентов mbo-robot-ui и market-robot-tms происходит в CD-pipeline:
https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/market-robot-stages


## Запуск на dev

Компоненты робота выкладываются на dev командой gradle uploadToDev. 
Код будет собран и залит в личную папку на aida

### Запуск robot-ui на dev

**1. Поменять порты**
* Перед выполнением uploadToDev открываем mbo-robot-ui-start.sh и ищем порты DEBUG_PORT, HTTP_PORT
* Меняем их на свои. Если порт не менять, робот запустится на 34804

**2. Выполнить uploadToDev**

`./gradlew :mbo-robot-ui:uploadToDev -Pproject.upload.host=aida`

**3. Добавить файл выгрузки в mbo-robot-ui_data**

Файл `https://sandbox.yandex-team.ru/task/1189423722/view`

После каждого uploadToDev выполняем на aida

`{your_login}@aida:~/dev/mbo-robot-ui_data$ sky get -pwu rbtorrent:f546dc0a54f2e0b298ea1c0bd45331baa68e76a1`

**4. Запуск и остановка сервиса**
* Запуск

`{your_login@aida}:~/dev/mbo-robot-ui$ ./bin/development/mbo-robot-ui-start.sh`
* Остановка

`{your_login@aida}:~/dev/mbo-robot-ui$ ./bin/development/mbo-robot-ui-stop.sh`

**5. UI и логи**

UI будет доступен по адресу

`http://aida.market.yandex.net:{HTTP_PORT}/robot/Robot.html`

Логи будут лежать по адресу:

`aida:~/{your_login}/logs/mbo-robot-ui/`

### Запуск robot-tms на dev

**1. Скрипты для запуска**

Для tms нужно добавить скрипты mbo-robot-tms-start.sh и mbo-robot-tms-stop.sh в ./bin/development/ аналогично mbo-robot-ui

При необходимости задать свои значения портов DEBUG_PORT, HTTP_PORT

`TODO` уточнить список параметров для mbo-robot-tms-start

**2. Выполнить uploadToDev**

`./gradlew :market-robot-tms:uploadToDev -Pproject.upload.host=aida`

**3. Запуск и остановка сервиса**
* Запуск

`{your_login@aida}:~/dev/market-robot-tms$ ./bin/development/market-robot-tms-start.sh`
* Остановка

`{your_login@aida}:~/dev/market-robot-tms$ ./bin/development/market-robot-tms-stop.sh`

**4. Проверка запуска tms на локальной машине**

1. Выполнить `./gradlew clean distTar`
2. Распаковать архив market-robot-tms/build/distributions/robot-tms.tar в любое место
3. Выполнить `./bin/robot-tms-start.sh`

Поможет понять, например, что все бины собрались

**5. Тестирование**

`TODO` Разобраться, возможен ли запуск тасков через telnet

**6. Логи**

Логи будут лежать по адресу:

`aida:~/{your_login}/logs/mbo-robot-tms/`

## Обновление зависимостей

Чтобы робот корректно подхватил последние версии зависимостей, выполняем

`./gradlew generateLock saveLock`

## Полезные ссылки в вики
**Настройка удаленного дебага** 

* backend

https://wiki.yandex-team.ru/market/mbo/development/onboarding/market-robot/#debagbekenda
* frontend

https://wiki.yandex-team.ru/market/mbo/development/onboarding/market-robot/#debagfronta

**Таблицы робота**

https://wiki.yandex-team.ru/market/development/datapreparation/robot/#osnovnyetablicyrobotaiixprednaznachenie

**Выкладка компонентов в обход пайплайна (в случае крайней необходимости)**
https://wiki.yandex-team.ru/market/development/datapreparation/ir-v-runtime-cloud/#vykladkakomponentov

## Возможные ошибки

Для Windows:
Если при запуске таски uploadToDev появляется ошибка 

`com.jcraft.jsch.JSchException: reject HostKey: <имя хоста>`, 

то в build.gradle заливаемого модуля следует добавить

```
ssh.settings {
  knownHosts = allowAnyHosts
}
```