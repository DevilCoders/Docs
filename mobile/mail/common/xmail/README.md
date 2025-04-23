## Монорепозиторий для Яндекс.Скрипта и его друзей ##

Весь код на Яндекс.Скрипте живет в этом проекте. Кроме того, прямо тут живет и обычный typescript-код, который использует 
модули Яндекс.Скрипта. Структура проекта
```
.
├── packages
|   ├── xpackages <Модули на Яндекс.Скрипте>
|   |   ├── common
|   |   |   └── code
|   |   |   |   └── ... <Транслируемый код>
|   |   |   xmail
|   |   |   └── code
|   |   |   |   └── ... <Транслируемый код>
├── ├── ys
|   |   └── ... <Сам Яндекс.Скрипт>
|   |
├── ios
|   └── Sources
|   |   └── xmail
|   |   |   └── generated-native-support
|   |   |   |   └── ... <Native mapped types, like YSArray, YSMap, etc. used by generated>
|   |   |   └── generated
|   |   |   |   └── ... <Files that are generated with `./generate.sh`>
|   |   |   └── native
|   |   |       └── ... <PAL libraries not used by generated and generated-native-support>
|   |   └── другие модули
|   └── Tests
|   |   └── ... <tests>
|   └── Package.swift -- Package config for Swift Package Manager. State external dependencies on Swift Frameworks here
|   └── .swiftformat  -- Set Swift formatting rules here. See https://github.com/nicklockwood/SwiftFormat for details.
├── android
|   └── Sources
|   |   └── xmail
|   |   |   └── dependencies
|   |   |   |   └── ... <Native mapped types, like YSArray, YSMap, etc.>
|   |   |   └── generated
|   |   |   |   └── ... <Files that are generated with `./generate.sh`>
|   |   |   └── native
|   |   |   |   └── ... <PAL libraries>
|   |   |   └── build.gradle -- Setup build rules here.
|   |   └── другие модули
|   └── Tests
|       └── ... <tests>
├── build-scripts
|   └── build-xplat.sh -- Генерация и интеграция кросс-платформенного кода в целевые проекты
├── generate.sh -- Use to transpile Common into platform languages.
├── setup.sh    -- Use to setup your environment
├── clean.sh    -- Removes all dependencies, so you can run `setup.sh` anew.
├── README.md   -- This file.
```

### Установка
- Устаналиваем arc, скачиваем аркадию и настраиваем automount https://wiki.yandex-team.ru/mobvteam/arc-macos/#ide
- Скачиваем WebStorm
- Открываем проект XMail в WebStorm. Он лежит по пути `mail/common/xmail`
- Устанавливаем последний `XCode` и `CommandLineTools`
- Устанавливаем зависимости проекта - запускаем конфигурацию `Setup Project` справа сверху
- Устанавливаем Android SDK и прописываем путь до него в `android/local.properties`. 
Пример: `sdk.dir=/Users/amosov-f/Library/Android/sdk`

### Запуск
Можно открыть терминал внизу WebStorm и воспользоваться следующими командами
- Обновление всех зависимостей во всех модулях `yarn`
- Юнит тесты `yarn test`
- Форматировавние, линтер и запуск юнит тестов `yarn flbt`

### Как устроены зависимости в кросс-платформенном коде
https://clubs.at.yandex-team.ru/xmail-xdisk/162


### Генерация кода
После изменении кросс-платформенного модуля надо перегенерить и переинтегрировать код для него и для всех модулей, 
которые от него зависят. Для этого можно воспользоваться скриптом `build-scripts/build-xplat.sh`. 
В качестве аргумента он принимает список модулей, которые надо перегенерить и переинтегрировать в целевые приложения.
Например, вывзов ```sh build-scripts/build-xplat.sh -m=mapi,xmail``` перегенерит код `mapi`, `xmail` и переинтегрирует все зависимости.
В этот список должны входить все модули, которые вы поменяли. Ключ `--skip-compiling` позволяет пропускать шаг с компиляцией kotlin и swift, 
а `--skip-integrate` позволяет не выполнять итоговую интеграцию сгенеренного кода в целевые приложения.
Для удобства, мы подготовили набор ран конфигураций в WebStorm, которые правильно вызывают этот скрипт и позволяют
- Перегенерировать только `xmail` - `Generate: I changed only xmail`
- Перегенерировать только `testopithecus` - `Generate: I changed only testopithecus`
- Перегенерировать только `eventus` - `Generate: I changed only eventus`
- Перегенерировать код для модулей из i-changed-modules.txt - `Regenerate code for i-changed-modules.txt (default ALL)`
В файле i-changed-modules.txt можно через запятую перечислить модули, которые вы поменяли. Если он пустой, то перегенерятся вообще все модули
Этот файл можно создать вручную, или он появится после первого запуска build-xplat.
- Перегенировать код всех модулей при помощи Docker-контейнера - `Regenerate code for i-changed-modules.txt (Docker)`
Эта конфигурация может быть полезна, если у вас винда, или вы не хотите заморачиваться с настройкой окружения для компиляции и интеграции сгенеренного кода
После сборки Docker-контейнера следить за генерацией можно во вкладке Attached Console. Файлы с ошибками появятся у вас на компьютере, 
только они будут иметь немного другие префиксы путей (можно искать без префикса /usr/src/arcadia)
Важно: пока эта таска только генерирует и компилирует код. Интеграция в целевые проекты будет сделана позже.

### Как добавить новый модуль
- Выполняем скрипт `sh build-scripts/module-template/new-module.sh new_module`, где `new_module` - имя нового модуля
- Добавляем модуль в `lerna.json`
- Добавляем модуль в корневой `package.json`
- Добавляем модуль в корневой Dockerfile
- Идем в `android/Sources/build.gradle` и добавляем туда `srcDirs += 'new_module'`
- Открываем `build-scripts/build-xplat.sh` и добавляем функцию `is_new_module_changed`, в которой описываем зависимости модуля, 
и функцию `integrate_new_module`, в которой прописываем, как надо интегрировать сгенеренные файлы в целевые приложения. 
Можно ориентироваться на примеры Android и iOS почты.
- В целевое Android приложение можно интегрировать код так: сделать модуль `xplat-new_module`, подключить его через gradle
и просто копировать туда файлы из `android/Sources/new_module`
- В целевое iOS приложение код можно интегрировать через Cocoapods 
   - с копированием в папку Pods, добавить в `Podfile` `pod 'new_module', :podspec => '../../../common/xmail/ios/new_module.podspec'`
   - без копирования в папку Pods, добавить в `Podfile` `pod 'new_module', :path => '../../../common/xmail/ios'`

По умолчанию, новый модуль зависит только от `common`. 
Все дополнительные зависимости надо прописывать в `ios/projects/new_module/Package.swift` (для локальной компиляции при генерации кода)
и в `new_module.podspec` для интеграции в целевое iOS приложение. Дополнительные зависимости для Android надо прописывать 
в `android/Sources/build.gradle` для локальной компиляции и потом в `build.gradle` модуля в целевом приложении.
Если вы интегрируете в Android свой первый модуль, то надо еще заинтегрировать туда еще и `common` - можно так же через модуль `xplat-common` (см. как в Почте)

Теперь, вы можете начать писать код на Яндекс.Скрипте в `packages/xpackages/new_module/code` 
и юнит-тесты для него в `packages/xpackages/new_module/__tests__/code`
Когда вы захотите сгенерить swift/kotlin код и сразу встроить его в ваши целевые iOS/Android приложения, выполните 
```
sh build-scripts/build-xplat.sh -m common,new_module,...
```

Важно! После рефакторинга и возможного перенесения кода в новый модуль надо проверить, что код в модуле `squeezer` не начал импортировать этот модуль.
Иначе надо будет поправить `prepare-squeezer-zip.sh`. TODO: сделать проверку на уровне сборки

### Таски в Тимсити 
[XMail::TestSandbox](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=MobileNew_Monorepo_Mail_Common_MailCommonXMailTestSandbox) - прогон линтера и тестов на исходном typescript-е
[XMail::BuildXPlat](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=MobileNew_Monorepo_Mail_Common_MailCommonXMailBuildXPlat) - 
генерит и компилирует весь код. Является обязательной для пул реквестов в `xpackages`
[XMail::IntegrateXPlat](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=MobileNew_Monorepo_Mail_Common_MailCommonXMailIntegrateXPlat) - 
генерит, компилирует и интегрирует код во все целевые приложения. Если вы по какой-то причине не можете настроить все окружения для `build-xplat.sh`,
то можете закоммитить исходный `.ts` код в ветку, после чего на **этой** же ветке запустить таску. Она правильно сгенерит, заинтегрирует код и закоммитит его в вашу ветку.
После чего вы можете сделать `git pull` и работать с кросс-платформенным новым кодом уже в целевых приложениях.

## Технические детали, как все работает

### Prerequisites
[Homebrew](https://brew.sh) is required to run `setup.sh`.
To install Homebrew one should either follow instructions on [Homebrew homepage](https://brew.sh), or simply run the following instruction in their terminal:
```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

To run iOS Podspec one will require [RVM](https://rvm.io), [Ruby](https://www.ruby-lang.org), and Bundler installed. `setup.sh` shell script should take care of that. However, you can follow the instructions in [Troubleshooting](#Troubleshooting), should the shell script fail.

### Installation
```
$ chmod +x ./setup.sh
$ ./setup.sh
```

### Usage
In `common` folder there's a `ys` folder that contains files that could be imported into target application files. They contain functions like `range` or types like `Nullable<T>`.

To generate `ios` and `android` files please use YS according to the following guide:
1) Edit files in `./common`
2) Run `./generate.sh` as follows:
```
$ ./generate.sh
```
3) iOS build logs can be found in `./ios/build.log`. The build results for iOS are in `./build/ios`.
4) Android build logs can be found in `./android/build.log`. The build results for Android are in `./android/Sources/build`.

`generate.sh` is capable of acting upon the generated artifacts, like xcodeproj file, or log files.
To run a command with the generated xcodeproj file, `-i` or `--ios` option should be used. If specified, the script will execute the passed command with the resulting xcodeproj file. E.g.
```
$ ./generate.sh -i=open
```
will open Xcode with the xcodeproj file.
To run a command with log files, please use `-l` or `--log` option, like so:
```
$ ./generate.sh -l=code
```
if you have VSCode installed, or
```
$ ./generate.sh -l=subl
```
if you have Sublime Text installed to open the log file in the specified editor.

The options can be used together:
```
$ ./generate.sh -l=code -i=open
```
will open Xcode with the project if the generation succeeds, or log file will be open in VSCode should the build fail.

For more details on how to use `generate.sh` please run it with `-h` option like:
```
$ ./generate.sh -h
```

#### Android Sample Project

- Open project in android subfolder using Android Studio
- Add Auth token and url path info into file ```x-mail.properties``` in the android/Sample folder, the format should be following:
```properties
token=<TOKEN_HERE>
x_mail_url=https://salavat.mailfront4.yandex.ru/api/mobile/v3
```
- Do some changes in non-generated code
- To bump library version and sync it with the sample project run bash script without params.
- If no version bump is needed - just run ```./sync.sh``` with any parameters, script will sync sample project with latest lib version
Example: ```./sync.sh -```
- Run "Sample" Configuration with emulator or real device as target and see changes applied

### Troubleshooting

#### RVM or Ruby version issues

RVM can be installed using the following command:
```
$ \curl -sSL https://get.rvm.io | bash -s stable
```
Having RVM installed, one should install Ruby:
```
$ rvm install ruby 2.6.3
```
Revisit the root directory of the project and, being there, please run:
```
$ bundler
```

#### Node version issues

In case there're issues with Node versions compatibility, there's a useful tool that helps managing Node versions: `nodebrew`. If the issue occurs, please use the said tool to install a working version.
The tool can be installed with Homebrew:
```
$ brew install nodebrew
```

Update your PATH env.variable:
```
export PATH="$HOME/.nodebrew/current/bin:$PATH"
```

To install a certain version of Node please use:
```
$ nodebrew install <version>
$ nodebrew use <version>
```
E.g:
```
$ nodebrew install 11.1
$ nodebrew use 11.1
```
Please note that if you have Node installed with Brew, it takes precedence, so you'll have to remove Brew Node installation: `brew uninistall --ignore-dependencies node`. `--ignore-dependencies` will keep Yarn intact.

#### Tests issues

If you observe tests failing at strange places (line number mismatch, errors are reported in code that is not in the source files, etc.), consider clearing Jest cache:
```
$ yarn run jest --clearCache
```
