# Тетя Роза

Сервис предсказания хорошести цены.

https://st.yandex-team.ru/RASPTICKETS-18063

## Локальный запуск
1. Нужна postgresql база, используется только на чтение, поэтому можно использовать [тестовую price-prediction](https://yc.yandex-team.ru/folders/foo1262pmfvsq72flh90/managed-postgresql/cluster/mdb9sssbmtcje8gtvlrc?section=databases)
1. `cp ./config/price_prediction.samples/config.development.yaml ./config/price_prediction/`
1. `vim ./config/price_prediction/config.development.yaml`
1. `./tools/run_dev.sh`
1. `grpcurl -v -emit-defaults -plaintext localhost:9001 list`
1. `grpcurl -vv -emit-defaults -plaintext -d '{"CheckPricesReq": {"1": {"PointFromKey": "c22", "PointToKey": "c213", "AdultSeats": 1, "Routes": "DP 262", "LocalDeparture": 1619393600, "Price": 2000}, "2": {"PointFromKey": "c22", "PointToKey": "c213", "AdultSeats": 1, "Routes": "DP 262", "LocalDeparture": 1619393600, "Price": 5000}, "3": {"PointFromKey": "c213", "PointToKey": "c65", "AdultSeats": 1, "Routes": "DP 262", "LocalDeparture": 1619393600, "Price": 4000}}}' localhost:9001 'ru.yandex.travel.avia.price_prediction.api.v1.CheckPriceService/CheckPrices'`

## Деплой
https://deploy.yandex-team.ru/projects/avia-price-prediction

## Сборка и выкатка
Собирается и выкатывается через ReleaseMachine
1. [Интерфейс](https://rm.z.yandex-team.ru/component/avia_price_prediction/manage?detail=job_results&scopes=3&branch=12&tag=1)
1. [Конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/release_machine/components/configs/avia/price_prediction.py)
1. При настройке деплоя нужно обязательно один раз проделать [следующее](https://wiki.yandex-team.ru/releasemachine/faq/#chtonuzhnosdelatchtobynauchitsjarelizitresursvya.deploy). Для того, чтобы при выкатке ресурса в sandbox, происходила выкатка в deploy.

## Генерация данных
1. [Описание](https://wiki.yandex-team.ru/avia/docs/xoroshie-ceny/)
1. [Код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/avia/price_prediction)

## TVM
1. [Пошаговая инструкция](https://wiki.yandex-team.ru/avia/devops/tvm/#poshagovajainstrukcijanastrojjkitvm-autentifikaciitd/qloud--priceprediction/deploy)

## Мониторинги и алерты
1. Используется [solomon-tool](https://a.yandex-team.ru/arc_vcs/travel/devops/solomon)
1. [Пошаговая инструкция](https://wiki.yandex-team.ru/avia/dev/solomon/#ispolzovaniesolomon-tool)
