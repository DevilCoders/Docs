# Приложение "Яндекс.Мессенджер"

## Использование

#### Актуальные версии

Актуальные версии всегда можно скачать через сервер дистрибуции по постоянным ссылкам.

**Внешнее приложение:**

- Windows: https://download.messenger.yandex.ru/desktop/latest?platform=win
- Mac OS: https://download.messenger.yandex.ru/desktop/latest?platform=mac

**Внутреннее приложение:**

- Windows: https://download.messenger.yandex.ru/desktop/latest?platform=win
- Mac OS: https://download.messenger.yandex.ru/desktop/latest?platform=mac
- Linux: https://download.messenger.yandex.ru/desktop/latest?platform=linux

#### Логи

Расположения логов для внешнего приложения:

- Windows: `C:\Users\%username%\AppData\Roaming\chats\logs\main.log`
- Mac OS: `~/Library/Logs/chats/main.log`

Расположения логов для внутреннего приложения:

- Windows: `C:\Users\%username%\AppData\Roaming\q\logs\main.log`
- Mac OS: `~/Library/Logs/q/main.log`
- Linux: `~/.config/q/logs/main.log`

#### Параметры запуска

- `--verbose` - открывает devTools и сыпит более подробные логи
- `--system-proxy-server` - разрешает использование системной прокси (например для отслеживания в Charles)

## Разработка

Для режима разработки необходимо запустить 2 части сборки:

1) Собрать статику приложения. Она собирается при помощи webpack и упаковывается сборщиком в само приложение. Это можно
   сделать командой `npm run app:webpack:dev team_chats -- --watch` - она будет собирать main-process и renderer-process в
   папку `./static` (у нас есть два скрипта `npm run app:webpack` для сборки продакшен билда и `npm run app:webpack:dev`
   для сборки с переменной окружения `NODE_ENV=development`. При ее добавлении сборка кэшируется и повторно собирается 
   быстрее, также это позволяет дебажить development билд через devtools)

2) Установить electron той же версии что в package.json глобально. (При запуске через локальную версию электрона мак не выдает права на доступ к keychain-у из-за чего не работает keytar) запустить из корневой директории электрон `NODE_ENV=development electron ./app/static --verbose`. Если возникнут проблемы с keytar, нужно запустить `npm run reset` из папки `./app`.

При пересборке статики renderer-process, достаточно просто перезагрузить страницу в приложении (Cmd+R, Ctrl+F5).
Если изменения произошли в main-process, то необходимо перезагрузить сам электрон.

## Сборка

Для полной сборки можно запустить скрипт `npm run app:build $APP_NAME`. В него можно передавать параметры для
electron-builder (см. ниже). Результатом будут собранные приложения в папке `/build`. В эту команду из
[секретницы](https://yav.yandex-team.ru/secret/sec-01df637w0athxsk3nwx4n0ghw1/explore/versions) подключаются
все секреты, которые необходимы для подписи приложения

По умолчанию будет собрано указанное вами приложение для текущей операционной системы, без подписи, будет
использовать локальную версию.

Собирать можно как локально, так и в docker-образе. Для этого необходимо указать переменную окружения
`BUILD_IN_DOCKER=true`, например так: `BUILD_IN_DOCKER=true npm run app:build $APP_NAME`.

Собранное приложение будет лежать в папке `./build`.

Что бы собрать релизную версию приложения, необходимо передать переменные окружения: `VERSION=1.0.0`
для указаний необходимой версии и `SIGN=true` для подписи.

Указать, для какой (каких) ОС необходимо проводить сборку, можно через параметры electron-builder.

Например, что бы собрать windows и linux для версии 2.0.0, необходимо выполнить команду:
`VERSION=2.0.0 SIGN=true BUILD_IN_DOCKER=true npm run app:build chats -- --win --linux`.

Mac версия корректно собирается в релиз, только на MacOS компьютерах, т.к. требует правильной сборки
dmg-файла и codesign. Пример для сборки релизного приложения:
`VERSION=2.0.0 SIGN=true npm run app:build chats -- --mac`.

### javascript-код

Базовая сборка кода проекта запускается командой `npm run webpack APP_NAME`.

Можно передавать все, что передается в обычный webpack, напр. `npm run webpack team_chats -- --watch` в режиме
пересборки при появлении изменений.

### electron-приложение

Базовая сборка всех приложений запускает електроном `npm run app:builder APP_NAME`

Сборка осуществляется при помощи утилиты [electron-builder](https://www.electron.build).

В таком виде, эта команда соберет 3 приложения для всех платформ.

Сборку можно конфигурировать через аргументы, которые принимает electron-builder.
Подробная документация доступна, запустив команду `npx electron-builder --help`.
Например, указать url сервера для обновления можно через параметр `--config.publish.url`:
`npm run app:build -- --config.publish.url=https://chat-app-test.s3.mds.yandex.net/app/test/`

По умолчанию сборку запустится прямо на компьютере. Так же сборку можно запустить в docker-контейнере,
определив это в переменной `BUILD_IN_DOCKER=true`. Это используется в CI (для сборки windows и linux),
а так же на машинах разработчиков, у которых не стоит полного набора необходимых утилит для сборки.

### Переопределение флагов при сборке
Переопределить флагов при сборке можно через переменную окружающей среды `OVERRIDE_RUNTIME_FLAGS`

```
OVERRIDE_RUNTIME_FLAGS="{\"enableWorkplace\": \"0\"}"
```
Доступно в sandbox задаче.

## Подпись приложений

Во всех режимах сборки, кроме релизной сборки в CI, мы ничего не подписываем. Если приложение
ругается на не надежный источник - если это не релиз, то это нормально.

Для подписи локально, необходимо:

- MacOS - установить ключи и запустить с параметром `--config.mac.identity="Yandex, LLC (477EAT77S3)"`. Сертификат доставляется на машину через sandbox ресурс.

- Window - подпись происходит через подписатор, процесс описан в файле [winSign.js](scripts/app/utils/winSign.js).
Подключение происходит через параметр `--config.win.sign="./scripts/app/utils/winSign.js"`

- Linux - не подписывается.

## Хранилище артифактов

В ходе сборки релиза, Sandbox и Trendbox CI собирают приложения и кладут их в тестовый bucket на S3.
Для того, что бы начать проверять с помощью сервера дистрибуции, необходимо выложить файлы в
основной внешний S3.

```bash
npm run app:deploy app_name/build_type/another_path
```

Так же можно указать bucket, через переменную окружения `BUCKET`, например:

```bash
BUCKET=messenger npm run app:deploy messenger/1.2.3
```

Для хранения собранных приложения используются:
- Для релизов: бакет `chat-app` и путь `_APP_NAME_/version/`
- Для пулл реквестов: бакет `chat-app-test` и путь `_APP_NAME_/pull/pull-number`

При релизе файлы приложений перекладываются в production bucket: chat-app

**Секретница:**
- https://yav.yandex-team.ru/secret/sec-01fs4v5z2hm1m8vhrwm00mv5kh

**Ресурсы:**

NVM (без ноды) `2718398582`
- [Resource link](https://sandbox.yandex-team.ru/resource/2718398582/view)
- [Download link](https://proxy.sandbox.yandex-team.ru/2718398582)

Кейчейн `2717919458`
- [Resource link](https://sandbox.yandex-team.ru/resource/2717919458/view)
- [Download link](https://proxy.sandbox.yandex-team.ru/2717919458)

Серт(P12 + CER) `2720678388`
- [Resource link](https://sandbox.yandex-team.ru/resource/2720678388/view)
- [Download link](https://proxy.sandbox.yandex-team.ru/2720678388)

**MAC сертификат**
!!Внимание!! Сертификат действителен до 12 января 2027го года, дальше сертификат нужно перевыпустить:

- Заводим [аналогичный](https://st.yandex-team.ru/APPMARKET-1430) тикет и получаем сертификат.
- [Собираем keychain](https://wiki.yandex-team.ru/browser/dev/infra/docs/dist/branded/macos-cert-update/#obnovleniesertifikatanojabr2021)
- Обновляем необходимые ресурсы и секреты

## Процедура сборки приложения в sandbox
Для сборки используется задача типа `MSSNGR_FRONT_ELECTRON_BUILD` [Код](
https://a.yandex-team.ru/arc_vcs/sandbox/projects/mssngrfront/tasks/MssngrFrontElectronBuild/__init__.py)

Задача сама по себе только доставляет данные из секретницы, ресурсы сэндбокса, env переменные настраивает arc и вызывает указанный в настройках скрипт.

Шаблон для запуска задачи сборки из `PR`: [ссылка](https://sandbox.yandex-team.ru/template/messenger_desktop_pr_4/view) (перед запуском измените номер пула)

Сборку можно запускать на агентах из группы [search_instrum-sandbox_mac_generic](https://c.yandex-team.ru/groups/search_instrum-sandbox_mac_generic) (возможно не нав всех, sandbox-mac** работали), нормальные агенты помечены user-тэгом `USER_MSSNGR_ELECTRON_BUILDER`

Для сборки необходимы следующие настройки:

Cекреты (YAV!!) (все переменные из этого раздела попапдают в env с прифексом `YAV_`):

`KEYCHAIN_PWD` - пароль от кейчейна

Ресурсы (все переменные из этого раздела попапдают в env с прифексом `RESOURCE_`):

`NVM` - айди ресурса с NVM
`KEYCHAIN` - айди ресурса с кейчейном

Что бы включить нотаризиацю:

Env:

`NOTARAIZE = 1` - включить нотаризацию

Yav:

`NOTARIZE_APPLE_ID` - айди аккаунта от которого будет происходить нотаризация
`NOTARIZE_APPLE_ID_PWD` - пароль от аккаунта

## Нотаризация

Приложение нотаризируется с помощью `electron-notarize` скрипт `app/scripts/afterSignHook.js`
Для запуска на агенте необходим xcode >= 10 (иначе будут проблемы с `xcrun altool`)

Для нотаризации используем нашего робота `robot-mssngr-builder`:
- Yandex-team аккаунт: https://yav.yandex-team.ru/secret/sec-01cxj4fx22apjqs63b4shxpr21/explore/versions
- ApplId + пароль (к аку привязан номер телефона tnovitskiy@yandex-team.ru): https://yav.yandex-team.ru/secret/sec-01fs4v5z2hm1m8vhrwm00mv5kh

## Сервер дистрибуция и обновление версий

Скачать актуальную версию:
- внешнюю: https://download.messenger.yandex.ru/messenger/desktop/latest
- внутреннюю: https://download.messenger.yandex-team.ru/messenger/desktop/latest

Указать новую версию для дистрибуции можно здесь:
- внешняя: https://bunker.yandex-team.ru/messenger-versions/dist/external/
- внутренняя: https://bunker.yandex-team.ru/messenger-versions/dist/internal/

"Сохраненная" версия доступна на тестовом сервере:
- внешняя: `download.messenger.test.yandex.ru`
- внутренняя: `download.messenger.test.yandex-team.ru`

"Опубликованная" версия на production сервере:
- внешняя: `download.messenger.yandex.ru`
- внутренняя: `download.messenger.yandex-team.ru`

Так же на сервере обновлений можно получить обновление до любой указанной версии
через путь `chat-app.s3.yandex.net/x.x.x/latest(-mac|-linux).yml`.

## Проверка обновлений

Любую сборку можно запустить в режиме обновления из альтернативного источника:

Переменные окружения для запуска приложений для тестирования обновлений:
* `REWRITE_UPDATE_INTERVAL` - интервал запроса обновлений, по умолчанию 5 минут;
* `REWRITE_UPDATE_URL` - URL сервера обновлений.

Сервера обновлений могут быть как инстансы distribution-server, так и просто пути в S3.

Приложение необходимо запускать с флагом `--verbose`, это позволит посмотреть лог обновления в консоли.

Пример проверки внутреннего приложения с тестового сервера на macOS:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://download.messenger.test.yandex-team.ru/desktop/update \
"/Applications/Yandex Team Messenger.app/Contents/MacOS/Yandex Team Messenger" --verbose
```

или через production сервер, но на указанную версию:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://chat-app.s3.yandex.net/team_chats/2.0.1 \
"/Applications/Yandex Team Messenger.app/Contents/MacOS/Yandex Team Messenger" --verbose
```

Пример проверки внутреннего приложения на Windows:
```bash
set REWRITE_UPDATE_INTERVAL=5000
set REWRITE_UPDATE_URL=https://download.messenger.test.yandex-team.ru/desktop/update
"C:\Users\%username%\AppData\Local\Programs\q\Yandex Team Messenger.exe" --verbose
```

или через продовый сервер, но на указанную версию:
```bash
set REWRITE_UPDATE_INTERVAL=5000
set REWRITE_UPDATE_URL=https://chat-app.s3.yandex.net/team_chats/1.2.3
"C:\Users\%username%\AppData\Local\Programs\q\Yandex Team Messenger.exe" --verbose
```

После скачивания обновления, в приложении должна появиться цветная плашка с кнопкой обновить.
После нажатия на кнопку, приложение должно перезапуститься.

**Важно:** в консоли не должно быть ошибок.

Пример неудачного обновления: https://paste.yandex-team.ru/709963

### Обновление на релизную сборку

Осуществляется подменой адреса обновления на адрес, содержащий необходимую версию,
с помощью переменной `REWRITE_UPDATE_URL`.

```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://download.messenger.yandex-team.ru/messenger/desktop/update/2.0.1 \
"/Applications/Yandex Team Messenger.app/Contents/MacOS/Yandex Team Messenger" --verbose
```

Пример для внешней версии:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://download.messenger.yandex.ru/messenger/desktop/update/2.0.1 \
"/Applications/Yandex Messenger.app/Contents/MacOS/Yandex Messenger" --verbose
```

Запускать необходимо на предыдущей релизной сборке. Она скорее всего доступна для скачивания
на production сервере дистрибуции: https://download.messenger.yandex-team.ru/messenger/desktop/latest

#### Альтернативный вариант с использованием тестового сервера:

Внутреннее приложение:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://download.messenger.test.yandex-team.ru/desktop/update \
"/Applications/Yandex Team Messenger.app/Contents/MacOS/Yandex Team Messenger" --verbose
```

Внешнее приложение:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://download.messenger.test.yandex.ru/desktop/update \
"/Applications/Yandex Messenger.app/Contents/MacOS/Yandex Messenger" --verbose
```

### Обновление с релизной сборки

Осуществляется подменой сервера обновлений на S3 путь, до специально собранной заведомо большой версии,
переменной `REWRITE_UPDATE_URL`.

Пример для внутренней версии:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://s3.mds.yandex.net/chat-app-test/messenger/internal/release/999.999.999 \
"/Applications/Yandex Team Messenger.app/Contents/MacOS/Yandex Team Messenger" --verbose
```

Пример для внешней версии:
```bash
REWRITE_UPDATE_INTERVAL=5000 \
REWRITE_UPDATE_URL=https://s3.mds.yandex.net/chat-app-test/messenger/external/release/999.999.999 \
"/Applications/Yandex Messenger.app/Contents/MacOS/Yandex Messenger" --verbose
```

Этот способ не работает для сборки из PR или ветки.

## Релиз

Для публикации релиза необходимо:
1) Переложить файлы приложений в production bucket на S3
2) Протестировать
3) Опубликовать версии в бункере.

Для перекладывания файлов релиза можно воспользоваться командой с указанием версии
`npm run release 1.0.0`. Переложены будут одновременно внутренние и внешние дистрибутивы.

Шаблон для ссылок на дистрибутивы для релизного тикета:

```markdown
⚠️ **Десктопные приложения v999.0.0**

**__Скачивание:__**

**External:**
Win: https://chat-app.s3.yandex.net/chats/999.0.0/Yandex_Messenger_Setup_999.0.0.exe
Mac: https://chat-app.s3.yandex.net/chats/999.0.0/Yandex_Messenger_Setup_999.0.0.dmg

**Internal:**
Win: https://chat-app.s3.yandex.net/team_chats/999.0.0/Yandex_Team_Messenger_Setup_999.0.0.exe
Mac: https://chat-app.s3.yandex.net/team_chats/999.0.0/Yandex_Team_Messenger_Setup_999.0.0.dmg
--Linux: https://chat-app.s3.yandex.net/team_chats/999.0.0/Yandex_Team_Messenger_999.0.0_amd64.deb--

**__Сервера обновлений:__**

**External:**
%%https://chat-app.s3.yandex.net/chats/9.9.9%%
**Internal:**
%%https://chat-app.s3.yandex.net/team_chats/9.9.9%%
```

Опубликовать версию можно в бункере, нажатием кнопки "Опубликовать":
- внешняя: https://bunker.yandex-team.ru/messenger-versions/dist/external/
- внутренняя: https://bunker.yandex-team.ru/messenger-versions/dist/internal/

## Ошибка NODE_MODULE_VERSION

```bash
Error: The module '/path/to/native/module.node'
was compiled against a different Node.js version using
NODE_MODULE_VERSION $XYZ. This version of Node.js requires
NODE_MODULE_VERSION $ABC. Please try re-compiling or re-installing
the module (for instance, using `npm rebuild` or `npm install`).
```

Эта ошибка возникает из-за того, что Electron использует собственную версию V8.

Для того, что бы исправить ошибку, достаточно запустить команду `npm run reset`, которая скачает необходимые на
данном компьютере бинарные файлы.

## Тестовые приложения

Для сборки и выкладки тестовых приложений необходимо локально запустить следующие команды:
```bash
npm run test-apps
```
