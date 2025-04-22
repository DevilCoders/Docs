## Базовая настройка проекта
1. Установите Homebrew ([Homebrew homepage](https://brew.sh/)). Обрати внимание, что brew должен располагаться в /opt/homebrew, чтоб дальнейшая инструкция работала.
2. Установите Java ``` brew install java11 ```
3. Установщик Java завершается предложением выполнить 3 команды. Они очень полезны, выполни их.
4. Установите RVM ([RVM homepage](https://rvm.io))
5. Перед тем как установить Ruby надо сделать ``` export optflags="-Wno-error=implicit-function-declaration" ```
6. Установите ruby через RVM. ``` rvm install 2.6.5 --disable-dtrace ```
7. Перезайдите в директорию проекта в консоли. RVM автоматически выставит правильную версию ruby и gemset
8. Установите Bundler `gem install bundler -v 2.3.4`
9. Установите все гемы из Gemfile `bundle install`
10. Необходимо установить Rugby (https://github.com/swiftyfinch/Rugby):
    - `brew install mint`
    - `mint install swiftyfinch/rugby`
    - После чего надо добавить mint в PATH - прописываем `export PATH=$HOME/.mint/bin:$PATH` в `~/.zshrc` и перезапускаем терминал 
11. Для первой сборки может понадобиться сделать `pod install`, чтобы перейти к следующему шагу
12. Установите поды специальной командой `./install_pods.sh -u`. Подробнее, почему так, можно почитать ниже, в разделе "Эстеншены диска".
13. Откройте воркспейс в Xcode `YandexDisk.xcworkspace`
14. Пройдите по ссылке и получите OAuth токен для стата https://oauth.yandex-team.ru/authorize?response_type=token&client_id=801af94c94e040848ebe206086a7a4e2 
15. Положите полученный токен в ~/.disk_stat_token
16. Скачай SwiftFormat https://github.com/nicklockwood/SwiftFormat/releases/tag/0.49.1 и Положи скачаный бинарь в ~/bin

Собранная статистика по билдам находится тут - https://stat.yandex-team.ru/Disk/Mobile/dev_build_benchmark_mobdisk_ios

Эти же шаги описаны в https://wiki.yandex-team.ru/users/artemida/okruzhenie-razrabotchika-mobdiska-na-apple-silicon/

## Kotlin Multiplatform

Диск использует Kotlin MM под капотом для ряда фичей. Если есть вопросы в этой части - приходи к artemida@

### Debug

Дебажить КММ можно из андройд студии. Для этого надо сделать следующие шаги:
1. Скаиваем Android Studio (https://developer.android.com/studio)
2. Заходим в Settings->Plugins, находим плагин Kotlin и Kotlin Multiplatform - устанавливаем оба.
3. Перезапускаем AS
4. Открываем как проект в AS файл arcadia/mobile/disk/common/build.gradle
5. В верхней панеле есть возможность выбрать текущую конфигурацию или отредактировать конфигурации(в выпадающем окне) - выбираем Edit configurations
6. В левом верхнем углу есть кнопка +, нажимаем ее (либо хоткей - Cmd+N) и выбираем iOS Application 
7. Указываем путь до workspace - arcadia/mobile/disk/ios/disk-app/YandexDisk.xcworkspace (не забудь в начале этого пути указать где у тебя лежит аркадия)
8. Выбираем схему - YandexDisk
9. Выбираем конфиг - Debug
10. Выбираем устройство. ВАЖНО!! пока мы не откажемся от розетовских симуляторов - мы не сможем дебажить мультиплатформу на симуляторах. Поэтому пока что работает только на девайсе.
11. Вы великолепны, расставляйте брейкпоинты(только по котлин коду) и работайте с дебаггером.

## Зависимости

### Установка подов
Диск использует для управления зависимостями Cocoapods - https://cocoapods.org. 
Third-party зависимости при этом предбилживаются и кэшируются на разработческих машинах посредством Rugby - https://github.com/swiftyfinch/Rugby/

Для удобства разработчиков есть единый скрипт для управления этой комбинацией - instal_pods.sh в корне mobile/disk/ios/disk-app.
По умолчанию данный скрипт инсталит поды (пострипанные для разработческой машины) и предсобирает их для DEBUG сборки. Существует два флага кастомизации:
-u - с этим флагом будет выполнен `pod install --repo-update`.
-t - с этим флагом зависимости будут предсобраны для конфигурации TEST, что позволит запустить unit тесты на разработческой машине.

### Создание новой pod
1. Для создания новых pod используем команду
```bash
pod lib create <PODNAME> --template-url=ssh://git@bb.yandex-team.ru/mobdisk/mobdiskios-pod-template.git
```
2. Добавляем файлы в Classes, удаляем папки Examples, Tests если они не нужны
3. Правим .podspec (name, version, summary, public_header_files). Если pod предназначен для телемоста, проверяем чтобы ios.deployment_target соответствовало телемостовой версии (11.0)
4. Копируем из последней выложенной подки (sic!) файлы fastlane/Fastfile, Gemfile, .ruby-version
5. Публикуем на Bitbucket
```bash
../../../common/tools/fastbuild/fastlane.sh publish_sdk s3AccessKey:"%ID_ACCESS_KEY%" s3SecretAccessKey:"%SECRET_ACCESS_KEY%"`
```
выбрать .podspec можно ключом ```podspec_file=Foo.podspec```
Токены можно взять дефолтные [robot-keanu-reaves](https://yav.yandex-team.ru/secret/sec-01e0d35mnhd7wp91qxy8htcvgs/explore/versions) или получить новые [instruction](https://wiki.yandex-team.ru/mds/s3-api/authorization/#sozdanieaccesskey)
pod появится тут: https://bb.yandex-team.ru/projects/MOBDISK/repos/mobile-disk-pods/browse

### Обновление pod
1. поднимаем version в Fastfile
2. публикуем так же как и при создании

## Эстеншены диска
В диске существует несколько экстеншнов - ShareExt NotificationServiceExt FilesExt FilesExtUI
Они съедают примерно четверть времени компиляции. Было принято решение, на дев машинах разрабатываться по умолчанию без них и подключать только при необходимости. Управлением экстеншнами занимается гем - configure_extensions. Для упрощения жизни его вызов обернут в два скрипта:
1. remove_extensions.sh
2. add_extensions.sh
Данный гем не удаляет экстеншны из проекта - только убирает их как депенденси из основного таргета. 
Команда pod install не умеет отрабатывать, если в Podfile перечислены экстеншны которые не имеют хоста с точки зрения файла проекта хкод. Поэтому для pod install у нас есть обертка - install_pods.sh, которая сначала подключает все экстеншны, выполняет установку подов, далее отключает экстеншны. 
В скрипт install_pods.sh можно передать флаг -u и тогда произойдет pod install --repo-update

## UI тесты
Работа с UI тестами описана в [UI Readme](./YandexDiskUITests/README.md)

## Обновление текстов
1. Добавляем API токен Танкера по инструкции https://tanker-guide.daas.yandex-team.ru/api/index.html
2. Для обновления запускаем скрипт ./Tanker/update_translations.sh
Чтобы внести изменения нужно править конфиг ./Tanker/tanker_conf.json. Это json с набором параметров и перечнем задач на синхронизацию. На данный момент доступна только один тип задач FetchTask на загрузку обновлений. В каждой задаче можно переопределить общие настройки (из корневого элемента json)

## SwiftFormat
Подтягивается через Cocoapods.
exec лежит тут `Pods/SwiftFormat/CommandLineTool/swiftformat`

Скрипт `swiftformatForChangedFiles.sh` в корне проекта запускает SwiftFormat для измененных файлов через git.

## Templates

Для создания фиче-модулей можно использовать шаблоны

### Установка шаблонов

Актуальная версия лежит в `/Resources/Templates`
Чтобы добавить актуальную версию шаблонов в Xcode нужно:
    - из папки проекта выполнить ```cp -r Resources/Templates ~/Library/Developer/Xcode/``` 
    (или самому скопировать папку Templates в `~/Library/Developer/Xcode`)

### Создание модуля из шаблона

1. Выбираем нужную папку и нажмаем Command + N
2. В окне выбора шаблонов скролим в самый низ и выбираем один из наших шаблонов (Module, Module+Table, ...)
3. Вводим название модуля, например `Sharing`
4. Выбираем нужную папку для модуля, если не сделали это на первом шаге и нажимаем `Create`
5. В выбранной папке должна появиться ссылка на папку модуля (потому что Xcode не создал для нее группы)
6. Нажимаем правой кнопкой мыши на выбранную папку (ту в которой лежит папка с модулем)
7. Выбираем пункт `Add Files to "YandexDisk"...`
8. Выбираем папку созданного модуля
9. Ставим галочку `Copy items if needed` и выбираем `Create groups`, затем нажимаем `Add`
10. В выбранной папке появляется нормальная папка с модулем
11. Удаляем ссылку на папку с модулем, которая появилась на 5 шаге выбрав опцию `Remove References`
