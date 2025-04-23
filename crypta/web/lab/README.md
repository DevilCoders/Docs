# Сборка и запуск

Поставить зависимости и собрать

    arcadia$ ya svn --detect up
    arcadia/crypta/ui/lab$ npm i

Собрать аркадией (сейчас не работает)

ya make -r . --checkout

Запустить тесты

    arcadia/crypta/ui/lab$ npm test

Запустить сервер для разработки

    arcadia/crypta/ui/lab$ HTTPS=true npm start

Запустить сервер для разработки c автоматическим прогоном тестов

    arcadia/crypta/ui/lab$ npm run test:watch

Собрать докер контейнер:

    arcadia/crypta/ui/lab$ make push
