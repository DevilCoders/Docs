# Код счётчика Метрики (work in progress)
Код счётчика Метрики v2

 * Публичная документация [по JS API](https://yandex.ru/support/metrika/code/counter-initialize.xml)
 * Документация по флагам в [browser-info](https://wiki.yandex-team.ru/jandexmetrika/doc/watchlog/)
 * Очередь в стартреке - [METR](https://st.yandex-team.ru/METR)
 * Карточка продукта [на вики](https://wiki.yandex-team.ru/jandexmetrika/)
 * Раздел про разработку [на вики](https://wiki.yandex-team.ru/jandexmetrika/frontend/watchjs/)

## Оглавление
- [Система контроля версий](#система-контроля-версий)
- [Установка](#установка)
- [Конфигурация](#конфигурация)
- [Пулл Реквест](#пулл-реквест)
- [Ручное тестирование](#ручное-тестирование)
- [Отладка под Android](#отладка-под-аndroid)
- [Отладка под iOS](#отладка-под-ios)
- [Отладка в BrowserStack](#отладка-в-browserstack)
- [Отладка в windows 10](#отладка-в-windows-10)
- [Тестирование Метрики для Турбоаппов](#тестирование-метрики-для-турбоаппов)
- [Тестирование gdpr плашки](#testirovanie-gdpr-plashki)
- [Утилита `bundle-diff`](#utilita)
- [Сборка ассессорского счётчика](#сборка-ассессорского-счётчика)
- [Релизный процесс](https://wiki.yandex-team.ru/JandexMetrika/frontend/watchjs/watchjs_release_process/)
- [Полезные ссылки](#полезные-ссылки)

## Система контроля версий
В качестве VCS используется Arc - система контроля версий Аркадии с интерфейсом git.

Хорошая документация и быстрый старт [описаны на wiki](https://wiki.yandex-team.ru/arcadia/arc/)

Для создания пулл реквестов понадобится утилита `ya`, [инструкция по установке](https://wiki.yandex-team.ru/JandexMetrika/frontend/how-to-install-ya/).

## Установка
Для уставки и сбора программы нужен [nodejs](https://nodejs.org/en/)

В самом простом случае достаточно, находясь в корневой папке проекта, выполнить команду
```
npm ci
```

Если установлен [nvm](http://nvm.sh), можно использовать нужную версию ноды:
```
nvm install && nvm use
```

## Конфигурация

### Хуки
[Ссылка на документацию](https://doc.yandex-team.ru/arc/manual/arc/hooks.html)

### Добавление новых хуков

Настройка хуков хранится в локальном конфиге арка, по умолчанию это `~/.arcconfig`.

**Можно пропустить все проверки ключом** `arc commit --no-verify`.
**Можно пропустить установку хуков** `HOOKS_SKIP_INSTALL=1 npm ci`.

## Пулл Реквест

Делаем при помощи `ya` - `ya pr create --merge --push --require=ship --publish --no-interactive`
( удобно сделать для этого alias ). Данная команда позволяет не только создать ПР но и запрещает его мержить
без хотя бы 1го аппрува ( `--require=ship` )

## Ручное тестирование
Для удобства тестирования на живых сайтах необходимо подменять реальные скрипты Метрики на локальные файлы.

Добиться этого можно с помощью proxy - программы, которая перехватывает исходящий http(s) трафик и позволяет как угодно его модифицировать.

Самая мощная proxy - [mitmproxy](https://mitmproxy.org/).

Для установки нужно выполнить:
```
pip3 install mitmproxy
```
Затем нужно выполнить минимальную сборку скриптов:
```
npm run build -- --bundle=debugProxy --files=tag.js watch.js
```
Эта команда должна собрать 2 скрипта, которые в дальнейшем будут использованы прокси. Эти скрипты должны появится по пути:
```
./_build/debugProxy/tag.ts ./_build/debugProxy/watch.js
```
Затем нужно запустить прокси с обработкой скрипта mitmproxy.py. Для этого нужно использовать команду:
```
npm run proxy
```
Эта команда запустит proxy сервер на порту 8888, который будет подменять запросы к скриптам Метрики на локальные файлы. Подробности можно найти в исходном коде mitmproxy.py
Затем нужно сконфигурировать свою операционную систему на использование proxy -
[mac](https://support.apple.com/guide/mac-help/enter-proxy-server-settings-on-mac-mchlp2591/mac) и
[win](https://www.dummies.com/computers/operating-systems/windows-10/how-to-set-up-a-proxy-in-windows-10/)

Для тестирования страниц требуется указать параметр в query string URL `_ym_debug=1`, например `https://www.mvideo.ru?_ym_debug=1`.

## Отладка под Android

Первым действием для того чтобы подменить watch.js на андройд-девайсе нам понадобиться android SDK, adb, и прочий софт для разработки.
Для того чтобы установить все эти полезные штуки разом проще всего скачать Android Studio.
После установки данных инструментов мы можем запустить прокси:

    npm run proxy

1) Если вы используете эмулятор идущий в комплекте с Android Studio, нажмите на пункт (...) в меню справа от девайса, перейдите во вкладуку Settings, затем в Proxy, выберите Manual proxy configuration, запишите 127.0.0.1 в инпут host и использующийся mitmproxy порт во вкладке port number.

2) Если вы используете "живой" android девайс вам понадобится usb кабель. Подключите девайс к вашей рабочей машине и активируйте usb-debug на девайсе.
В настройках нужно зайти в меню "about system", 7 раз тапнуть на версию сборки, затем в появившемся пункте "development" можно включить дебаг и авторизовать вашу машину.
На рабочей машине выполните команду

```adb reverse tcp:xxxx tcp:yyyy```

Где yyyy - порт используемый mitmproxy, а xxxx - любой порт на вашем телефоне через который пройдёт проксирование.
Далее выберите wifi к которому вы подключены и в настрйках прокси введите localhost:xxxx.


Теперь вам необходимо установить на ваш девайс сертификат mitmproxy.
Для этого перейдите на сайт [mitm.it](http://mitm.it) на вашем девайсе или эмуляторе и скачайте и установите нужный сертификат.

## Отладка под iOS

### На симуляторе (только на mac)
1. Ставим xcode последней версии через AppStore (вместе с ним установится simulator)
2. Убеждаемся что mitmproxy стоит актуальной версии, если же нет, обновляем её, включаем прокси, устанавливаем размещение для wi-fi и скачиваем сертификат с [mitm.it](http://mitm.it)
3. Скачиваем следующую утилиту для митмпрокси:
```git clone https://github.com/ADVTOOLS/ADVTrustStore.git```
4. Переходим в папку и выполняем следующую команду
```./iosCertTrustManager.py -a <путь к скачанному сертификату mitmproxy-ca-cert.pem>```
5. Запускаем симулятор с интересующим нас девайсом и версией ios, заходим в Settings > General > About > Certificate Trust Settings и включаем наш корневой сертификат
6. (Опционально) если вы хотите отлаживать визор и локально записывать его визиты, зайдите в настройки Safari и отключите Prevent cross-site tracking (дев сервер склеивает сессии по 3rd party cookie)
7. Открываем сафари, находим наш девайс в меню разработки и открываем дебаггер для интересующей нас страницы. Для дальнейшей отладки шаги с установкой сертефикатов повтортять не надо, достаточно просто включить девайс и установить нужное размещение для wi-fi.

### На живом девайсе

1. Ставим прокси на общедоступном домене (jkee.org) или внутреннем сервисе
2. Настраиваем прокси в настройках wi-fi или сотовой сети. На сервис где есть прокси
3. Подменяем трафик и выводим отладочную информацию прямо на сайт

## Отладка в BrowserStack

1. На сервисе находим бинарник ['Test websites ... proxies'](https://www.browserstack.com/local-testing/live) ![alt](https://jing.yandex-team.ru/files/erdmko/2020-03-02T13%3A22%3A55Z.png)
1. Запускаем локальную проксю ```npm run proxy```
1. Запускаем стенд с интересущим браузером ищем там ключ ![alt](https://jing.yandex-team.ru/files/erdmko/2020-03-02T13%3A25%3A47Z.png)
1. Дописываем к ключу данные прокси
```./BrowserStackLocal <key> --local-proxy-host localhost --local-proxy-port 8888  --force-proxy --force-local```
1. Доверяем сертификату ![alt](https://jing.yandex-team.ru/files/erdmko/2020-03-02T13%3A31%3A27Z.png)

## Установка под windows 10

1. Ставим [Ubuntu](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
2. Перезагрузить
3. Ставим [Анакоду](https://www.anaconda.com/download/#linux) через wget
4. Ставим зависимости OS ```sudo apt-get install build-essential libssl-dev libffi-dev python-dev python-pip libxml2-dev libxslt-dev git```
5. Создаем окружение в анаконде ```conda create --name myenv```
6. Включаем окружение ```source activate myenv```
7. Ставим pip в conda ```conda install pip3```
8. Ставим mitmproxy ```pip3 install mitmproxy```
9. Качаем репозиторий, включаем прокси

## Тестирование Метрики для Турбоаппов

### Начальная установка и настройка

- Нужно скачать apk последнией сборки турбоаппа с [TeamCity](https://teamcity.browser.yandex-team.ru/buildConfiguration/Browser_AndroidBuilds_ReleaseBuilds_Internal?branch=master-20.2.2%2Fandroid%2Frc&buildTypeTab=overview)
    - В последнем коммите идем в _Successful build_
    - Скачиваем Artifacts ⇢ apks ⇢ <дата>.<айдишник>-yandexbrowser-arm64-stable-api21-internal-release.apk
- Установка При помощи adb
    - [Скачиваем adb](https://developer.android.com/studio/releases/platform-tools) ( Download SDK Platform-Tools for * )
    - Можно сразу добавить adb в `$PATH` или засунуть под alias, но это не обязательно
    - [Устанавливаем приложение](https://www.online-tech-tips.com/smartphones/how-to-install-apps-on-your-android-device-from-your-computer/) c adb
- Настройка Турбоаппа
    - Нужно лонгтабнуть по логотипу в главном меню ( он находится сразу над строкой поиска )
    - Откроется модалка
    - Во вкладке FEATURES
        - найти turbo_apps, везде проставить галочку где она не стоит, **а также** где ставим галочку нажать Overwritten
        - найти chinese_menu, нажать на Overwritten
    - Нажать на кнопку перезагрузить ( круглая со стрелочками в правом нижнеи углу )
    - Зайти в настройки и заинейблить отладку по USB ( Settings ⇢ DEVELOPER TOOLS ⇢ Debugging Web Pages using USB )

## Тестирование gdpr плашки
Для использования тестовой версии плашки нужно запустить прокси с переменной ```gdprPopupProxy```:
```
gdprPopupProxy=true npm run proxy
```

### Chrome Developer Tools

Если для отладки или тестирования нужны chrome developer tools, вот [тут](https://developers.google.com/web/tools/chrome-devtools/remote-debugging) подробная интсрукция по настройке

P.S. Иногда не видит с первого раза, в таком случае достать USB и вставить обратно

### Подключение Снифера

Снифер помогает прослеживать весь HTTP / HTTPS траффик для девайса

- Если на устройстве еще не настроен PDAS, нужно настроить, [мануальчик](https://wiki.yandex-team.ru/diy/android/pdas/)
- Подключится к WI-FI сети PDAS
- Настройка прокси для PDAS на телефоне
    - В настройках в разделе WI-FI лонгтаб по PDAS ⇢ Modify
    - В настройках пркси выставить Manual
    - Proxy Hostname ⇢ `metrika01k-dev.man.yp-c.yandex.net`
    - Proxy Port ⇢ `8888`
- На телефоне, идем на [http://mitm.it/](http://mitm.it/) и скачивам сертификат ( без его, сниффер не пропускает HTTPS трафик )
- Затем нужно включить сам снифер
    - В нашем любимом проекте ⇢ [.../metrika/frontend/watch](https://a.yandex-team.ru/arc/trunk/arcadia/metrika/frontend/watch)
     собираем бандл для турбоаппов ⇢ `npm run build -- --bundle=prod`
    - Включить Снифер ⇢ `npm run sniffer`
    - Если не удобно смотреть запросы в терминале, есть GUI версия ⇢ `npm run sniffer:gui`
    - Снифер должен логировать все HTTP / HTTPS запросы на метричные домены и подменять `tag.js` на `tag_turboapp.js`

## Утилита `bundle-diff`

При помощи `npm run bundle-diff` можно посмотреть что удалилось / добавилось в базовом бандле.

При вызове команды происходит следующее:

- собирается текущий базовый бандл
- делается `arc checkout HEAD~1`
- собирается базовый бандл из предыдущего коммита
- делается `arc checkout` назад в текущую бранчу
- прогоняется либо `git diff --no-index` либо Node.js based утилита чтобы показать diff

Все собранные бандлы, а также сам diff будут лежать в `_build/.temp`.

Поддерживаются следующие CLI аргументы:

- `--cache` - показывает diff с последнего прогона не пере-собирая бандлы ( доступно как `npm run bundle-diff:cache` )
- `--noColor` - отключает цвета
- `--commitsToCheckout` - определяет на сколько коммитов откатываться, чтобы собрать бандл с которым сравнивать текущий
  ( значение от сюда подставляется в `arc checkout HEAD~...` )
- `--filter` - по-умолчанию `bundle-diff` показывает diff целиком. К сожалению часто случается так, что части кода просто
  передвигаются с места на место, что делает сложным понять что именно изменилось в бандле. Эта опция заставляет `bundle-diff`
  скрывать линии, которые были сначала добавлены, а потом сразу же удалены, т.е. _передвинуты_
  ( доступно как `npm run bundle-diff:filter` )
- `--file` - файл для которого посмотреть diff. Например, для `tag_turbo.js`: `npm run bundle-diff -- --file=tag_turbo.js`
 ( или `npm run bundle-diff:turbo` ). Файл должен быть в списке файлов для бандла `nofeat` в папке `@mappings`.

## Утилита `bundle-size`

При помощи команды `npm run size -- [options]` можно посмотреть как изменился размер бандла. Это помогает при контроле того, как новый код повлиял на размер файлов. Данный скрипт используется в CI для вывода информации о изменении размера файлов в виде комментария в ПР в Arcanum.

При вызове команды происходит следующее:

- собирается текущий базовый бандл
- проверяется размер полученных файлов
- размер выводится в файл `bundleSize.json`
- по завершении процесса бандл удалется из папки `_build`

Поддерживаются следующие CLI аргументы:

- `--bundle` - название бандла для сборки. Дефолтное значение - `nofeat`.
- `--files` - список файлов для сборки (в качестве разделителя используется запятая или пробел). Дефолтное значение - это список всех файлов для заданного бандла (для базового бандла `nofeat` список будет таким: `no_feat.js,tag_turbo.js`). Важно, что здесь названия файлов передаются с расширением, аналогично команде `npm run build`.
- `--no-delete` - флаг указывающий на то, что собранные файлы не надо удалять по завершении процесса. Без флага папка бандла будет удалена.

### Примеры использования

Сборка определённого файла в базовом бандле:
```bash
npm run size -- --files tag_turbo.js
```
Сборка определённого бандла:
```bash
npm run size -- --bundle prod
```
Сборка определённых файлов в заданном бандле:
```bash
npm run size -- --bundle prod --files tag.js watch.js zzlc.html
```
Сборка определённых файлов в заданном бандле с запретом удалять папку с бандлом после завершения команды:
```bash
npm run size -- --bundle prod --files tag.js watch.js zzlc.html --no-delete
```

## Сборка ассессорского счётчика

1. Собрать в sandbox таск METRIKA_ARCADIA_WATCH_BUILD, указав нужную ветку из аркадии в параметре "URL Аркадии", например - arcadia-arc:/#users/stanislavsky/METRIKASUPP-12482. Запустить таску и дождаться её завершения.
2. Зайти в полученном таске во вкладку resources и скопировать айди ресурса METRIKA_WATCH. Склонировать [таск YA_PACKAGE](https://sandbox.yandex-team.ru/task/817978964/view), изменив в Adhoc packages id ресурса на скопированный. Указать custom version как 1.{id таски YA_PACKAGE}. Запустить таску и дождаться её завершения.
3. Клонировать [таску](https://c.yandex-team.ru/tickets/1992988) в кондукторе и изменить версию на полученную на предыдущем шаге выкладки.
4. Проверить выложен ли [assessor-tag.js](https://yastatic.net/metrika-static-watch/assessor-tag.js).

## Полезные ссылки

1. [Сборка](https://wiki.yandex-team.ru/jandexmetrika/operations/watchdeploy2d/)
2. [Релизный процесс](https://wiki.yandex-team.ru/JandexMetrika/frontend/watchjs/watchjs_release_process/)
3. [Декодер](https://codepen.io/arinteck/pen/qBjBqEZ?editors=0011)
