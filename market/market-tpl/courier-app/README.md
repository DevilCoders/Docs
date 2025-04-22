[![oko health](https://badger.yandex-team.ru/oko/repo/market-mobile/market-tpl-app/health.svg)](https://oko.yandex-team.ru/repo/market-mobile/market-tpl-app)

# Подготовка среды

Для разработки мы используем **Arc** - систему контроля версий Аркадии, хранящую данные в облаке и использующую
виртуализацию рабочей копии. Если впервые об этом слышишь, пройди [курс](https://moe.yandex-team.ru/courses/my/course/1272)

Для настройки среды надо установить:

- Android Studio: скачать из Self Service
- WebStorm или VSCode (любимую IDE для разработки JS части): скачать из Self Service
- [Brew](https://brew.sh/index_ru)
- [Arc клиент и плагины для IDE](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
- Java SDK:

  ```
  brew install openjdk@11

  sudo ln -s $(brew --prefix)/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
  ```

- Node.js: `brew install node`
- Watchman: `brew install watchman`

# Установка

Получить исходный код и установить npm-пакеты:

```
arc mount -m ~/arcadia -S ~/store
cd ~/arcadia/market/market-tpl/courier-app/
npm install
npx jetify
```

В данном примере рабочее дерево будет смонтировано в каталог `~/arcadia`, а локальное состояние репозитория
и скачиваемые данные будут хранится в каталоге `~/store`

#Настройка Android Studio

Добавьте переменные окружения выполнив:
(если используется zsh .bash_profile заменить на .zprofile)

```
cat <<EOT >> ~/.bash_profile
export PATH="/usr/local/bin:$PATH"
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:/Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home/bin
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
EOT

source ~/.bash_profile
```

В настройках(⌘,):

- Appearance & Behavior → System Settings → Android SDK -> SDK Platforms
  ![SDK Platforms](docs/sdk_platforms_settings.png)
- Appearance & Behavior → System Settings → Android SDK -> SDK Tools
  ![SDK Platforms](docs/sdk_tools_settings.png)

Если скачивание `Intel x86 Emulator Accelerator (HAXM installer)` падает с ошибкой, нужно [cкачать архив](https://dl.google.com/android/repository/extras/intel/haxm-macosx_v7_6_5.zip), разархивировать, и выполнить в корне архива:

```
sudo su

source ./silent_install.sh
```

Ресурсы по настройке

- [Настройка Android Studio](https://reactnative.dev/docs/environment-setup)
- [Настройка эмулятора](https://charles-stover.medium.com/create-a-react-native-app-on-an-android-emulator-1c0d94f288ae)

# Дополнительные шаги

Для запуска под android необходимо [поставить сертификат на эмулятор](https://wiki.yandex-team.ru/Market/3pl/development/fronts/).

Если проект не собирается, выполните в корне:

```
echo sdk.dir=$HOME/Library/Android/sdk > local.properties
```

# Запуск android

Запустить настроенный виртуальный девайс

В терминале войти в папку с проектом ( `cd ~/arcadia/market/market-tpl/courier-app/` ) и выполнить:

```
npm run clean-start
```

Открыть еще одно окно терминала и выполнить в папке с проектом:

```
# Для девайсов с гугл-сервисами
npm run google

# Для девайсов с хуавей-сервисами
npm run huawei
```

После этого апк установится на ваш девайс/эмулятор. Запускаем приложение!

# Сборка Android

## Релизный .apk локально:

```
npm run generate-apk
```

После выполнения команды собранный .apk файл будет находиться в папке `android/app/build/outputs/apk/release/`

# Автотесты

Одному тест кейсу должен соответствовать один тестовый класс. Это связано со спецификой перезапуска тестов. Список упавших тестов (имена классов) собираются в текстовый файлик для последующего перезапуска.

В автотестах мы используем [TUS](https://wiki.yandex-team.ru/test-user-service/). До запуска теста берем из сервиса свободный аккаунт, гоняем на нем тест, после прогона отпускаем аккаунт для других тестов. Большинство тестов можно наследовать от BaseTest с переопределением метода prepareData, также в нем уже есть поле с uid текущего курьера.
На момент написания, вручную заведено 10 курьеров. Если вдруг 10 курьеров будет мало, можно добавить новых (добавить аккаунт в TUS, завести курьера и расписание).

при необходимости можно реализовать:

- [ ] использование тегов в аккаунтах tus, нужно для тестов dbs или других специфичных юзеров
- [ ] автоматизация создания автотестовых курьеров

## Запуск автотестов локально

Рабочий эмулятор для запуска автотестов:

![img_2.png](docs/e2e_emulator.png)

### Токен для получения курьеров

Для хождения в tus нужно получить [токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9052de6e4cf142039a7ee44ac03e4614).
Чтобы пользоваться нашими аккаунтами, нужен [доступ](https://idm.yandex-team.ru/system/test-user-service/roles#f-status=all,f-role=test-user-service/tus_market_tpl_app/user,sort-by=-updated,f-is-expanded=true,f-state=granted), выдан группе `Разработка (Курьерская Платформа)`
Подтянуть токен можно двумя способами:

1. положить токен в файл `local.properties`, например:

   ```properties
   tus_token=AQAD-xxxxxxxxxxxxxxxxxxxxxxxxxxx
   ```

   после этого нужно синхронизировать проект с гредл

   ![img_1.png](docs/gradle_sync.png)

   и проверить, что токен подтянулся (в конфигурации / Instrumentation arguments)

   ![img.png](docs/instrumentation_arguments.png)

2. Либо вручную вводить в настройках теста:

   1. Нужно выбрать тест который хотим запустить. Например: `android/app/src/androidTest/java/ru/yandex/market/tpl/courier/test/DropshipOutOfTurnGoBackTest.kt`

   2. Заходим в этот файл, правой кнопкой мыши нажимаем на имя класса и выбираем пунк _Create DropshipOutOf..._

   3. В появившемся окне оставляем всё без изменений, кроме _Instrumentation arguments_: нажимаем _"…"_, в окне _Instrumentation Extra Params:_ нажимаем _"+"_, чтобы добавить аргумент (в sandbox эти параметры берутся из e2e.config.yaml):

      - в поле _name_ пишем `tus_token`, а в поле _value_ - сам токен.

      - Нажимаем _ОК_, _OК_

### Чтобы запустить тест:

1. В терминале из корня проекта запускаем `npm start`
2. Открываем в Android Studio нужный тест, нажимаем слева от имени класса кнопку со стрелками и выбираем _Run..._

   ![img.png](docs/run_e2etest_android_studio.png)

### Возможные проблемы и их решения:

1. `DefaultFailureHandler$AssertionFailedWithCauseError: '(view has effective visibility <VISIBLE> and view.getGlobalVisibleRect() covers at least <100> percent of the view's area)' doesn't match the selected view`

   **Решение:** Помог запуск на другом эмуляторе android 10 и 29 api

### Просмотр allure отчетов в PR:

1. В PR ищем проверку "**Прогон автотестов**" и нажимаем на нее
   ![img.png](docs/at_check_in_pr.png)
2. Попадаем в teamcity и переходим на вкладку Allure Report
   ![img.png](docs/tc_allure_report.png)

### Просмотр allure отчетов локально

1. Прогнать тест(ы)
2. в терминале выполнить команду: `cd android/ && ./gradlew allurePull && ./gradlew allureServe`

возможные проблемы: `OException: Cannot run program ".../projects/market-tpl-app-v2/market-tpl-app/android/null/platform-tools/adb`
**решение:** установить **android_home** в переменные окружения, например, добавить в bash_profile:

> export ANDROID_HOME=/YOUR_PATH_TO/Android/sdk

### Просмотр http запросов на эмуляторе:

1. в build.gradle.kts установить `ENABLE_CHUCKER true`
2. После этого при запуске теста будут собираться все логи походов в сеть, а посмотреть их можно в строке уведомлений эмулятора, нажав на соответсвующее уведомление
3. Не забудьте отключить этот флаг перед коммитом.

### Возможные причины падения DBS автотестов:

Если у курьера не завершена смена, автотесты будут падать, до тех пор пока мы не перейдём на TUS (MARKETTPLAPP-882).

##### Решение:

Проверить завершена ли смена мы можем по такому запросу в базе: select \* from user_shift where user_id = 81569; Все смены должны находится в статусе SHIFT_FINISHED
Если нет, то мы можем поправить это только руками, проставляем смене статус SHIFT_CLOSED и завершаем эту смену через ручку /manual/user-shifts/finish

# Процессы

Разработку ведем в пользовательских "фича" ветках и по готовности делаем PR в trunk.
**Перед созданием PR не забудь сделать rebase на обновленный trunk**
Для автоматического мержа PR должен быть включен тумблер Automerge, и выполнены все проверки:

- Пройдено код ревью
- В ПР прилинкован тикет и тикет должен быть в статусе "закрыт" или "ждет релиза"
  [список допустимых статусов](https://a.yandex-team.ru/arc_vcs/market/market-tpl/courier-app/a.yaml#L26)
- Пройдены проверки TS, ESlint, Jest
- Прошла дебаг - сборка
- Прошли автотесты, если автотесты упали, надо проверить отчет, если тест просто флапнул, то перезапустить прогон автотестов (кнопка "против часовой стрелки" Restart рядом с названием проверки), если изменения сломали функциональность, починить

Чтобы изменения попали в релиз они должны быть в транке, в большинстве случаев тестировщики переводят тикет в статус "ждет релиза" сами после завершения тестирования
