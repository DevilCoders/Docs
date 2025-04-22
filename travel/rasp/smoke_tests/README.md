Смоук-тесты для проектов Расписаний. Ходят по ручкам в заданные окружения и проверяют статусы ответов.
Используются для минимальной проверки живости окружения.

Запускаются в sb вот так: https://st.yandex-team.ru/RASPFRONT-9875#615c0edc8b446568b4bb9f63

Тесты написаны на py3.7 + pytest.

Запуск тестов:
```
1) Установить переменные окружения RASP_SMOKE_TEST_CONFIG (обязательно), RASP_SMOKE_TEST_ENV, RASP_SMOKE_TEST_ENVPARAMS, RASP_SMOKE_TEST_STABLENESS
export RASP_SMOKE_TEST_CONFIG=export
export RASP_SMOKE_TEST_ENV=production
export RASP_SMOKE_TEST_ENVPARAMS="host=prestable.morda-backend.rasp.yandex.net"
export RASP_SMOKE_TEST_STABLENESS=stable  # если не установить - запустит все

2) Собрать бинарник тестов из корня проекта (при этом произойдет параллельный запуск тестов)
ya make -tt

Можно указать количество чанков для распараллеливания (по дефолту 10)
ya make -tt -D RASP_SMOKE_SPLIT_FACTOR=5

После сборки можно перейти в директорию с собранным бинарником и запустить его без пересборки (тесты будут выполняться последовательно)
cd bin/tests
./travel-rasp-smoke_tests-bin-tests --config=morda_backend --env=production --envparams="host=prestable.morda-backend.rasp.yandex.net" --stableness=stable
```

Для винды:
```
0) Запустить в консоли
arc mount -m path\to\arcadia\mount\point

1) Установить переменные окружения RASP_SMOKE_TEST_CONFIG (обязательно), RASP_SMOKE_TEST_ENV, RASP_SMOKE_TEST_ENVPARAMS, RASP_SMOKE_TEST_STABLENESS
set RASP_SMOKE_TEST_CONFIG=export
set RASP_SMOKE_TEST_ENV=production
set RASP_SMOKE_TEST_ENVPARAMS="host=prestable.morda-backend.rasp.yandex.net"
set RASP_SMOKE_TEST_STABLENESS=stable

2) Собрать бинарник тестов из корня проекта (при этом произойдет параллельный запуск тестов)
ya make -tt

Можно указать количество чанков для распараллеливания (по дефолту 10)
ya make -tt -D RASP_SMOKE_SPLIT_FACTOR=5

```

Есть и готовая сборка для запуска в Докере:
```
1) поставить докер
2) получить токен от яндексового реестра образов тут:
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
3) залогиниться в реестр
docker login -u <доменный юзер> -p <токен из п.2> registry.yandex.net
4) скачать образ
docker pull registry.yandex.net/rasp/smoke-tests
5) запуск
docker run -it registry.yandex.net/rasp/smoke-tests --config=morda_front --env=testing -v -ra -n2

Пример с перегрузкой параметров:
docker run -it registry.yandex.net/rasp/smoke-tests --config=morda_backend --env=production -v -ra -n2 --envparams="host=prestable.morda-backend.rasp.yandex.net"

Полезные параметры:
--lf - запустить последние сломанные тесты
--fulltrace - вывести полный трейсбек, если тест сломался

```
- На Маке есть большие [проблемы с ipv6 в докере](https://wiki.yandex-team.ru/users/monitorius/Docker-IPv6-OSX/), так что просто так тесты проходить не будут. Лучше запускать на Убунте либо без Докера.
- [Дока про реестр](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)

Запустить с подключением локальной папки smoke_tests - чтобы можно было локально менять код, а запускался он в докере:
```
docker run -it -v /Users/monitorius/work/rasp/smoke_tests/smoke_tests:/app/smoke_tests registry.yandex.net/rasp/smoke-tests --config=morda_front --env=testing
```

Зайти в консоль контейнера, не запуская тестов (для дебага)
```
docker run -it registry.yandex.net/rasp/smoke-tests --config=morda_backend --env=production -v -ra -n2 --envparams="host=https://prestable.morda-backend.rasp.yandex.net"
```


Собрать и залить образ можно так:
```
docker build -t smoke-tests .
docker tag smoke-tests registry.yandex.net/rasp/smoke-tests && docker push registry.yandex.net/rasp/smoke-tests
```


[Пример билда в Teamcity](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Rasp_MordaFront_Tests_SmokeTestsProduction)
