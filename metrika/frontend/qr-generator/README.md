# Скрипты

`npm run watch` — запуск проекта  
`npm run build` — сборка проекта  

#Обновление тестинга
1) `npm run release:test`

# Релиз
1) Увеличиваем версию с помощью команды `npm run ver-inc`. Команду возможно выполнить с указанием уровня изменения версии (major, minor, patch, premajor, preminor,
   prepatch, or prerelease).
2) Собираем релизный билд и выкладываем статику с помощью команды `npm run release:prod`. 
Для запуска необходимо настроить профиль AWS, либо передать ENV-переменные `AWS_SECRET_ACCESS_KEY` и `AWS_ACCESS_KEY_ID`. Получить секреты можно [здесь](https://yav.yandex-team.ru/secret/sec-01cq6h5rtj649gg8h94zwqshc8/explore/version/ver-01fgv109httyx5572zwargfntd).
3) Поменять в [апстриме](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/qr/upstreams/list/qr/show) версию статики на 14 строке на загруженную 

# Стенды
Тестинг: https://qr-test.yandex.ru/
Прод: https://qr.yandex.ru/
