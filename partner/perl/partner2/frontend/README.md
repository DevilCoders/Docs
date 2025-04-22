./frontend
-----

Здесь все, что относится к фронтенду.

Установка
=====

    npm install
    ./node_modules/.bin/bower install

Также, в Makefile родительской директории определен таргет `lego_install`, который делает вышеперечисленное:

    make lego_install

Сборка
=====

Конфигурация находится в файле `buildConfig.js`.

Сборка с помощью [Grunt][grunt]'а:

    grunt build                  # сборка, таск по умолчанию
    grunt clean                  # очистка
    COMPRESSED=false grunt build # сборка в devMode и без компрессии
    grunt watch:build            # ожидание изменений в исходниках и сборка
    grunt watch:test             # ожидание изменений в исходниках и запуск тестов

В `../Makefile` описаны следующие таргеты:

    make lego                  # сборка
    make lego_clean            # очистка
    make lego_clean lego       # пересборка
    COMPRESSED=false make lego # сборка в devMode и без компрессии
    make lego_watch            # ожидает изменения в файлах, если есть - запускает сборку

Тесты
=====

Тесты находятся в папке `./test`. Структура произвольная, но просьба придерживаться здравого смысла при группировке.

В качестве библиотеки тестов используется [Mocha][mocha], для ассертов - [Chai][chai].
Запуск тестов:

    grunt test       # разово запускает все тесты
    grunt watch:test # ждет изменений в файлах, после чего запускает тесты

Также, доступны следующие таргеты в `../Makefile`:

    make lego_test       # разово запускает все тесты
    make lego_watch_test # ждет изменений в файлах, после чего запускает тесты


Как работает сборка
=====

BEM
-----

[ENB][enb] собирает три бандла – *priv*, *common* и *promo*:

 - *priv* – содержит серверный bemhtml и локализованные строки
 - *common* – содержит клиентский js, bemhtml, стили и строки для основного сайта
 - *promo* – содержит клиентский js, bemhtml, стили и строки для главных страниц

Конфигурация сборки находится в файле `.enb/enb-make.js`.

Порядок сборки такой:

 - из нужных шаблонов `.bem.tt2` генерируется *BEMJSON* (см. технологию в файле `.enb/techs/tt2bemjsom.js`):

     * вырезаются теги *TT2*
     * полученный *BEMJSON* склеивается в массив `([{}, {} ... {}])`

 - из полученного *BEMJSON* генерируется *bemdecl*, из него *deps.js*
 - по имеющимся зависимостям в *deps.js* генерируются файлы соответсвующих технологий (priv.js, js, css, i18n)

Результат складывается в папке `.tmp`.

Для бандла *priv* используются шаблоны в файлах `require('buildConfig').allTemplates`, для *common* – шаблоны, определенные в `require('buildConfig').clientTemplates`, для *promo* – в `require('buildConfig').promoTemplates`

JS
-----

Далее все *priv.all.priv.js*, *commmon.{lang}.js* и *promo.{lang}.js* обрабатываются [LMD][lmd], который добавляет возможность использования CommonJS-like модулей (*require*). Конфиги находятся в `.lmd/`.

*common.{lang}.js* и *promo.{lang}.js* обрабатываются [Borschik][borschik]'ом (с компрессией, если переменная окружения `COMPRESSED` не равна `false`).

`priv.all.priv.js` помещается в `../common.priv.js`, клиентские скрипты - в папку `../data/js/`.

CSS
-----

Обрабатывается [Borschik][borschik]'ом. Результат помещается в папку `../data/css/`.


[grunt]: http://gruntjs.com/
[mocha]: http://visionmedia.github.io/mocha/
[chai]: http://chaijs.com/
[enb]: http://enb-make.info/
[lmd]: http://lmdjs.org/
[borschik]: http://bem.info/articles/borschik/
