Инфраструктура Геоплатформы
===

[Вики-страница](https://wiki.yandex-team.ru/geo-infra/)

| Директория | Описание |
--- | ---
[apiteka](apiteka) | Сервис для выдачи api-ключей, проверки подписей запросов и лимитирования
[auth_agent](auth_agent) | Nginx-плагин + локальный агент для выписывания tvm user-тикетов / получения user-info
[balancer_deployer](balancer_deployer) | Инструмент для деплоя конфигурации балансеров из Аркадии в AWACS
[baseimage](baseimage) | Базовый докер-образ Геоплатформы для сервисов в Няне ([документация](baseimage/README.md))
[capacity](capacity) | Инструменты для автоматизации задач capacity-planning Геосервисов
[conserva](conserva) | Система создания бэкапов S3-бакетов в YT ([документация](https://docs.yandex-team.ru/conserva/))
[duty](duty) | Инcтрументы для управления дежурствами в Гео ([документация](duty/readme.md))
[ecstatic](ecstatic) | Cистема доставки данных в картах ([документация](https://docs.yandex-team.ru/ecstatic/))
[environment_linker](environment_linker) | Библиотека для проставления симлинок на конфиги в соотв. с окружением
[masquerade](masquerade) | Сервис для подменты креденшиалов юзеров на фейковые при зеркалировании в тестинг
[metric_collector](metric_collector) | Утилита для сбора yasm-метрик из нескольких источников ([документация](metric_collector/README.md))
[monitoring](monitoring) | Инструменты для мониторинга сервисов: упрощают жизнь дежурным, считают SLA, проверяют результаты нагрузочных стрельб
[pycare](pycare) | Асинхронный веб-фреймворк на базе aiohttp для создания веб-сервисов на python3
[quotateka](quotateka) | Сервис для управления rps-квотами ratelimiter2
[ratelimiter2](ratelimiter2) | Сервис для ограничения частоты запросов на распреленном кластере ([документация](https://wiki.yandex-team.ru/geo-infra/ratelimiter2-manual/))
[recipes](recipes) | Рецепты для ya.make
[roquefort](roquefort) | Инструмент для сбора метрик с nginx'а и отправки в yasm ([документация](roquefort/README.md))
[sandbox](sandbox) | Инструменты для создания бинарных sandbox-задач с возможностью релиза через sedem
[sedem](sedem) | Cистема управления жизненным циклом сервисов ([документация](https://docs.yandex-team.ru/sedem/))
[tanks](tanks) | [Документация](tanks/README.md) про сервис с танками для нагрузочного тестирования
[teacup](teacup) | Сервис для тестирования базового образа, принимает трафик от чайника
[teapot](teapot) | Сервис для тестирования базового образа, генерирует траффик для кружки
[teaset](teaset) | Мета-сервис для тестирования базового образа ([документация](teaset/README.md))
[teaspoon](teaspoon) | Мини-сервис для тестирования релизов через sedem
[tvm2lua](tvm2lua) | Nginx-плагин для выписывания и валидации tvm service-тикетов ([документация](tvm2lua/README.md))
[yacare](yacare) | Fastcgi-фреймворк для создания веб-сервисов на c++ ([документация](yacare/README.md))
