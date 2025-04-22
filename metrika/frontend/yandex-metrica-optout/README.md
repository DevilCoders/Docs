# yandex-metrica-optout
Расширение позволяет отключить метрику на сайтах.

Технически ставит глобальную переменную `Ya._metrika.oo = true;`, а код счётчика на неё смотрит.

# Установка
Клонируем репозиторий

    git clone git@github.yandex-team.ru:Metrika/yandex-metrica-optout.git

В папке с проектом запускаем

    npm i
    npm run build

После чего в папке `_build` появляется файл и папка. , `*.zip` - для браузеров, поддерживающих WebExtension (chrome/яб/opera/vivaldi/firefox). Папка `*.safariextension` - для сафари

# Переводы и танкер
Переводы хранятся в проекте `metrika`, кейсет `opt-out-extension`.

Для обновления переводов нужно запустить

    npm run i18n

# Выкладка
### [Chrome](https://h.yandex-team.ru/?https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdeveloper%2Fdashboard%3Fhl%3Dru "Chrome store")
Логин: metrika.dev@gmail.com

Пароль: ghbdtnklov0

### [Firefox](https://h.yandex-team.ru/?https%3A%2F%2Faddons.mozilla.org%2Fru%2Fdevelopers%2Faddons "Firefox store")
Логин: metrika.yndx@yandex.ru

Пароль: m}OM-s8D^e0QBHU

### [Opera](https://h.yandex-team.ru/?https%3A%2F%2Faddons.opera.com%2Fdeveloper%2Fbeta%2F "Opera store")
Логин: metrika-yndx
Почта: metrika.yndx@yandex.ru
Пароль: P<C]499l+g[]p]U

### Safari
У Сафари нет своего стора, поэтому собранный пакет нужно хранить у себя на сервере.

Точнее [стор](https://h.yandex-team.ru/?https%3A%2F%2Fsafari-extensions.apple.com) есть, но только в качестве галереи, загрузка расширения идет с сервера автора.

Активируем режим разработчика: Safari->Настройки->Дополнения->Ставим галочку «Показать меню разработка»

Для подписи расширения нужно иметь Apple dev аккаунт. Для это пишем ramzes или egolotvin. Затем по адресу [https://developer.apple.com/account/safari/certificate/](https://h.yandex-team.ru/?https%3A%2F%2Fdeveloper.apple.com%2Faccount%2Fsafari%2Fcertificate%2F) создаем сертификат, ждем подтверждения от egolotvin, скачиваем сертификат и устанавливаем к себе в keychain

![скрин](https://jing.yandex-team.ru/files/rifler/2016-06-23_18_16_24.png)

В Сафари открываем Extension Builder, добавляем папку _build/@metrics-opt-out-extension.safariextension и жмем `Создать пакет`. Картинка:

![скрин](https://jing.yandex-team.ru/files/rifler/2016-06-23_18_20_24.png)

Заливаем к себе на сервер. Не забываем добавить в MIME тип `.safariextz`

Пример для nginx

    types {
        .....
        application/octet-stream safariextz
        .....
    }



Для Apache

    AddType application/octet-stream .safariextz

Чтобы залить расширение в галерею, идем на [эту страницу](https://h.yandex-team.ru/?https%3A%2F%2Fdeveloper.apple.com%2Fsafari%2Fextensions%2F) и следуем инструкциям.

### TODO
Сделать Update Manifest URL - Сафари периодически ходит по этому урлу и проверяет версию текущего установленного плагина и по урлу. Если нужно - обновляет.

## ...to be continued...
