# mobile-autoru-client-android  
Android-клиент приложения autoru  

<details><summary>Сборка на teamcity</summary>
</p>

Сборка на [teamcity](https://teamcity.yandex-team.ru) происходит через [sandbox](https://sandbox.yandex-team.ru/), подробнее можно прочитать в [посте](https://clubs.at.yandex-team.ru/android-dev/400) или на [wiki](https://wiki.yandex-team.ru/mobvteam/sandbox-runner/)


Для сборок мы используем несколько конфигов:
* `config/rc.config.yaml` - служит только для сборки релиз-кандидата
* `config/stat_checks.config.yaml` - прогон статчеков (lint/detekt)
* `config/test_app.config.yaml` - сборка testapp
* `config/unit_tests.config.yaml` - прогон unit-тестов
* `config/common.config.yaml` - для всего остального (универсальная конфигурация)

Во все конфиги gradle-команды прокидываются через параметр `sandbox.env` на teamcity, так что менять команды можно прямо из конфигурации на teamcity

  
</details>

<details><summary>Пулл реквесты и код ревью</summary>  
</p>

  - [Описание работы с ПР'ам и ревью находится тут](https://wiki.yandex-team.ru/vsapps/autoru-mobile/android_team_processes/)  
  
</details>

<details><summary>Сборка на удаленной машине</summary>  
</p>
Мы используем mainframer и mirakle (рекомендованно) для build'а на удаленной машинке.  

## mainframer  
[тут инструкция](https://wiki.yandex-team.ru/users/tagakov/setup-mainframer/)  
  
По сути все, что нужно сделать, это поставить плагин BashSupport, зайти в терминал и вбить  
`./mainframer-init.sh`  
а потом билдить через опцию remote build (cmd +alt + r —> remote build — run)  
Если нужно обновить конфиги запуска в IDE, то можно запускать с параметром  
`./mainframer-init.sh -skip_remote`  
  В таком случае выполнятся только локальные настройки  
  
## mirakle  
[страница на гитхаб](https://github.com/Instamotor-Labs/mirakle)  
  
Как настроить:  
  
Запустить скрипт
`./mirakle_init.sh`

Добавить файл
~/.gradle/init.d/mirakle_init.gradle  
  
```groovy  
initscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "com.instamotor:mirakle:1.2.0"
    }
}

// need to perform it before we set plugin: Mirakle, or gradle.taskNames will return [mirakle]
def areTestsEnabled = areTestsEnabled(gradle)

if (isMirakleEnabled(gradle)) {
    apply plugin: Mirakle
}

rootProject {
    if (isMirakleEnabled(gradle)) {
        mirakle {
            host "android-build-01-sas.dev.vertis.yandex.net"
            if (areTestsEnabled) {
                println("Sync will take more time as here we have a task with test")
                excludeRemote += ["src", "/build/android-profile"]
            } else {
                println("You are not running tests now, sync will be optimized")
                excludeRemote += ["src", "build/tmp", "build/kotlin", "/build/android-profile", "build/intermediates"]
            }
            rsyncToRemoteArgs += ["--compress-level=1"]
            rsyncFromRemoteArgs += ["--compress-level=4"]
        }
    }
}

static def isMirakleEnabled(gradle) {
    return gradle.startParameter.projectProperties.containsKey("mirakleEnabled")
}

static def areTestsEnabled(gradle) {
    def tasks = gradle.startParameter.taskNames
    def hasTest = tasks
            .findAll { !it.contains("testapp") }
            .any { it.toLowerCase().contains("test") }
    return hasTest
}
```  
В Preferences -> Build, Execution, Deployment -> Compiler -> Command-line options добавить флаг -PmirakleEnabled.  
Для ускорения можно добавить еще флагов:  
-PdevSdk=21 --parallel -Pkotlin.incremental=true --stacktrace -PmirakleEnabled
  
Убедиться, что выключен instant run, удалена папка .mainfraimer.  
  
После изменений синкнуть гредл, и пользоваться студией, как пользовались до мейнфреймера — вся работа будет происходить на удаленной машинке.

Известные проблемы:

Фейлится компиляция на Dagger'е. Лечение:
* подключиться к удаленной машине ssh <see-build-log-to-get-host>
* удалить ~/.gradle
* удалить ~/mirakle/{project}
* удалить локально {project}/build и {project}/app/build
* исполнить локально ./gradlew clean
* запустить сборку
</details>

<details><summary>Скрипты и полезняшки лежат в директории /scripts</summary>

* **`open-deeplink.sh`** быстро открывает диплинки через adb. `-p` или `--prod` для того чтобы открыть диплинк в продовом аппе (по умолчанию используется packagename дебажного аппа)
* **`paste-to-device.sh`** вставляет содержимое буфера в текстовое поле на девайсе/эмуляторе
* **`update-dicts.kts`** обновляет словарики с расшифровкой параметров фильтров. Для работы требуется [kscript](https://github.com/holgerbrandl/kscript)
* **`pull-http-trace.kts`** работает вместе с TraceRule в тестах. Позволяет вытащить записанные рулой JSON ответы сервера и переложить в структуру папочек, готовую для копирования в ассеты тестов 
* **`pull_screenshots.sh, push_screenshots.sh`** - скачать тестовые скриншоты с девайса или наоборот, запушить на девайс
* **`get_screenshots.main.kts`** - выбирает из отчёта скрины и предлагает сразу их rsync-нуть в директорию со скринами проекта.

    **Примеры:**
    scripts/get_screenshots.main.kts --daily 52312871 - выгрузить из дейли билда 52312871
    scripts/get_screenshots.main.kts --stable 52313181 --rsync - выгрузить из стейбл билда 52313181 скрины и сразу засинкать их, пропустив диалог
</details>

<details><summary>Оплата тестовой картой</summary>
</p>

* Для оплаты покупки тестовой картой необходимо следовать [инструкции](https://yookassa.ru/developers/using-api/testing)
* Необходимо убедится, что в конфигурационной шторке выставлен параметр "Тестовый магазин для оплаты"

</details>

<details><summary>Добавление эксперимента в AB</summary>
</p>

Эксперимент содержит ключ (название эксперимента) и значение (в данный момент на клиенте поддерживаются числовые и boolean значения), с помощью которого клиент варьирует поведение.

Чтобы добавить эксперимент, нужно выполнить следующие шаги:
* Завести выборку в AB по этой [инструкции](https://wiki.yandex-team.ru/vsapps/autoru-mobile/yandexabios/) (см. раздел "Как завести выборку")
* Добавить эксперимент на клиент:
  * Завести одноименный ключ эксперимента из выборки в **ExperimentKey** (ключ не чувствителен к регистру)
  * Добавить дефолтное значение для эксперимента в класс **DefaultExperimentsConfigurator**
* Дальше значение эксперимента можно получать через **ExperimentsManager.instance.get(ExperimentKey)** по ключу

</details>

<details><summary>Скриншотные тесты</summary>

Для запуска скриншотных тестов есть два способа: 
1. Создана конфигурация screenshotTests, в её настройках можно указать имя класса теста и если нужно - имя метода. Не работает с miracle. Не позволяет указать в студии девайс, в контексте которого будут выполняться тесты.
2. Через интерфейс студии (кнопка запуска слева от класса/метода теста)
![image](https://jing.yandex-team.ru/files/aleien/2022-05-12_09-47-31.png)<br/>
Для работы этого способа нужно перед тестами выполнить скрипт `scripts/push_screenshots.sh`. 
После тестов, если нужно было сгенерировать новые эталоны - выполнить `scripts/pull_screenshots.sh`, а для перепроверки - снова `scripts/push_screenshots.sh`.

Настройки эмулятора для скриншотных тестов: API 31 1080x1920 420dp 5", в пресетах студии это Pixel 2
![image](https://jing.yandex-team.ru/files/aleien/2022-05-12_09-49-18.png)

**ВАЖНО!**
---
Единственное изменение нового эмулятора, которое необходимо сделать - это выставить настройку:
`hw.mainKeys = yes` 
Сделать это нужно перед запуском эмулятора вручную в файле `~/.android/avd/[название эмулятора]/config.ini`. Эту папку можно открыть  из студии:
![image](https://jing.yandex-team.ru/files/aleien/2022-05-12_09-50-07.png)
Так же лучше обновить chrome (может падать во время выполнения тестов)



Чтобы сгенерировать новые эталоны в замен старым, нужно удалить их с последующей выгрузкой на устройство и прогнать нужные тесты. Для новых тестов нужно прогнать тесты, скачать скриншоты 
и запушить их снова на эмулятор.
`sh scripts/pull_screenshots.sh`
`sh scripts/push_screenshots.sh`

</details>
