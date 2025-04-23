# Сборка и запуск

Поставить зависимости и собрать

    arcadia$ ya svn --detect up
    arcadia/ads/ml_monitoring/ui$ npm i && ya make -r . --checkout

Запустить тесты

    arcadia/ads/ml_monitoring/ui$ npm test

Запустить сервер для разработки

    arcadia/ads/ml_monitoring/ui$ npm start

Запустить сервер для разработки c автоматическим прогоном тестов

    arcadia/ads/ml_monitoring/ui$ npm run test:watch

Собрать докер контейнер:

    arcadia/ads/ml_monitoring/ui$ make push
