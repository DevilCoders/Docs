# Обновление браузеров

 - [Selenium Grid](#selenium-grid)
 - [Karma](#karma)

## Selenium grid

Chrome установлен на машине `chrome-node.haze.yandex.net`, **Firefox** — на машине
`phantomjs-node.haze.yandex.net` (это не опечатка).

1. Если у вас не настроен доступ к этим хостам по ключу, настройте его по
[инструкции](https://beta.wiki.yandex-team.ru/lego/selenium-grid/auth/).

1. Зайдите на сервер по ssh

 ```sh
 ssh -i ~/.ssh/haze ubuntu@firefox-node.haze.yandex.net
 ```

1. Скачайте нужную версию браузера ([Firefox](https://ftp.mozilla.org/pub/mozilla.org/firefox/releases/),
 [Chrome](http://dist.yandex.ru/yandex-precise/unstable/amd64/))

1. Распакуйте дистрибутив

 ```sh
 # для firefox
 tar -jxf firefox-31.0.tar.bz2
 ```
 ```sh
 # для chrome
 ar p google-chrome-stable_37.0.2062.120-1+yandex0_amd64.deb data.tar.gz | tar zx ./opt
 ```

1. Скопируйте распакованное в `/opt/{browser}/versions/{version}`

 ```sh
 # для firefox
 mv firefox /opt/firefox/versions/31.0
 ```
 ```sh
 # для chrome
 mv ./opt/google/chrome /opt/chrome/versions/37.0
 ```

1. Для **Chrome**: выставьте права доступа к файлу `chrome-sandbox`

 ```sh
 sudo chown root.root /opt/chrome/versions/37.0/chrome-sandbox
 sudo chmod 4755 /opt/chrome/versions/37.0/chrome-sandbox
 ```

1. Создайте скрипт-обертку для запуска браузера по образу и подобию в
 `/opt/{chrome,firefox}/bin`

1. По образу и подобию добавьте секцию про новую версию браузера в
`/etc/selenium-grid/selenium-node.json`

1. Перезапустите **selenium-node**

 ```sh
 sudo initctl restart yandex-selenium-node
 ```

После того, как всё настроено, сделайте новый **snapshot** с этих машин в
[интерфейсе](http://haze.yandex-team.ru).


## Karma

1. Укажите новые версии браузеров в [enb-islands-tools](https://github.yandex-team.ru/lego/enb-islands-tools/blob/master/karma.conf.js#L86-L99).

1. Выпустите *patch*-версию пакета (она должна подхватиться всеми библиотеками в автосборке автоматически).
