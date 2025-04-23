Приложение для предустановок на Samsung, Oppo и пр.
Представляет из себя ярлык ведущий в GP, точнее по market://details?id=ru.yandex.disk

## Сборка
Сборка на TC не налаживаем, т.к. нужно собирать крайне редко. Скорее всего даже один раз
Команда сборки локально выглядит так
```
sh monomainframer.sh "DISK_RELEASE=true BUILD_NUMBER=1 METRIKA_PROD_KEY=MMM trackingId=TTT ./gradlew installer:assembleRelease"
```
где МММ - это ключ прод метрики (смотри на TC),
а ТТТ - это 891724537899590157, который был заведен [специально для предустанок](https://appmetrica.yandex.ru/campaign?appId=18895&campaignId=891724537899590157)
