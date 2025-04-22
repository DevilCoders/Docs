## Установка

Клонируем репозиторий

    git clone git@github.yandex-team.ru:Metrika/informer.git informer

Ставим зависимости

    cd informer
    npm i

Запускаем

    npm start

Теперь при изменении файлов будет пересобираться `_build/informer.js`

Для сборки `production` билда запускаем

    npm run build

## Тестирование

Ставим `Yaxy` глобально, если еще не

    npm install yaxy -g

Читаем доку про настройку и все такое - [https://github.com/Kolyaj/Yaxy](https://github.com/Kolyaj/Yaxy)

Пример конфига

    $SetDocumentRoot /Users/rifler/Documents
    $UseSSLFor mc.yandex.ru
    mc.yandex.ru/metrika/informer.js => file://~/_build/informer.js
        $SetResponseHeader Content-Type: application/javascript; charset=UTF-8

    mc.yandex.ru => $
    $SetResponseHeader Strict-Transport-Security: 0

Теперь запрос к [скрипту информера](https://mc.yandex.ru/metrika/informer.js) должен отдавать несжатый скрипт с локальной машины вместо оригинального

После этого можно тестировать на каком-нибудь продакшен сайте или создать локальную страницу и вставить туда код счётчика с информером.
