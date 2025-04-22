# MJ Framework

**MJ Framework** (aka Mary Jane, aka Microservice Java Framework) — это инструменты для генерации кода микросервиса и готовые клиенты для работы с внешними сервисами.

**Решаемые задачи**
- Минимизация необходимости написания бойлерплейт кода
- Упрощение написания кода с помощью готовых заглушек
- Снижение порога входа для разработки
- Унификация кода, логов, взаимодействия между сервисами

## Фичи
* **[Кодогенерация контроллеров](pages/features/controller.md)** - на основе файла [api.yaml](pages/how_it_works/configuration/api_yaml.md) в формате OpenAPI.
* **[Кодогенерация клиентов](pages/features/clients.md)** - генерация клиентов к другим сервисам по openapi спецификации. Сгенерированные клиенты основаны на библиотеке [common-retrofit](https://a.yandex-team.ru/arc/trunk/arcadia/market/jlibrary/common-retrofit) с [asynchttpclient](https://github.com/AsyncHttpClient/async-http-client). Есть возможность настройки с помощью модулей [resilience4j](https://resilience4j.readme.io/docs/retrofit).
* **swagger** - у сервиса будет доступен swagger ui с описанием ручек (по пути `/swagger-ui`)
* [**TVM**](pages/features/tvm.md) - имеется возможность указания своего tvm id, tvm id сервисов, куда сервис собирается ходить. Для своих api имеются настройки для отключения tvm или использования user ticket на определенных ручках. Все это можно настроить для разных сред. Сервис для работы с tvm добавится в BUILD_ROOT. В сгенерированных клиентах и контроллерах будет необходимый код для работы с ними.

* **Трассировки** - в сгенерированных клиентах и контроллерах уже есть необходимый код, отписывающий трассировки
* **Ручки /ping и /monitoring**

* **Готовые модули кода** - в сервис можно добавить готовые модули для определенных сценариев работы (напр. для работы с postgres)
* **Готовые/пользовательские run configurations в idea** - для запуска и регенерации проекта
* **ya project** - MJ [интегрирован](pages/ya_project.md) в команды создания/обновления исходного кода [ya project create/update](https://docs.yandex-team.ru/ya-make/usage/ya_project)

## Стрельбы сервиса на MJ
[Здесь](https://wiki.yandex-team.ru/homepage/strelbypomjframework/) можно почитать результаты стрельб по сервису на MJ.

## Дальнейшие планы
**Q4 2021**
- Сбор фидбека, правки
- Заглушки и необходимое окружение для тестов
- Попробовать договориться с devtools по поводу ya make или плагина
- Другие библиотеки/модули (например, unified agent, logbroker)
- Server side rate limiter
- Проработка локального старта
- **Возможно** Проперти для модулей в service.yaml
- Можете накидать нам еще идей :)

**Q1 2022**
- Работаем с devtools над интеграцией в ya и плагин для idea
- Обновление версий Spring Boot и не только
- JOOQ
- Метрики JMX и spring-actuator
- Solomon Agent

[Подробный бэклог](https://st.yandex-team.ru/filters/gantt/order:/all/month/none/Sat%20Jan%2001%202022%2003:00:00%20GMT+0300%20(Moscow%20Standard%20Time)/filter:423575 )

## Записи демо
- [Запись демо альфа-версии фреймворка 20.07](https://jing.yandex-team.ru/files/myhellsing/GMT20210720-130515_Sergey-Fedoseenkov-s-Personal-Meeting-Room_1760x900.mp4)
- [Запись со встречи 17.08 (бета-версия фреймворка)](https://jing.yandex-team.ru/files/myhellsing/zoom_0-2.mp4)

## Как контрибьютить
Код лежит [тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/mj/v1), а стартеры [вот тут](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/spring-boot-starters).
Перед пулл реквестом нужно прийти [в наш чат](https://t.me/joinchat/RImGNXqbohFkOTg6) и посоветоваться, как лучше делать ту или иную фичу. Если повезет, то мы ответим, что фича уже у нас в работе.

После этого можно создавать пулл реквест. Если в пулл реквесте находится новая фича, то ее надо описать в [документации](https://a.yandex-team.ru/arc/trunk/arcadia/market/infra/java-application/mj/docs).

Ревьюеры из нашей команды назначатся автоматически. А если нет, то можно пнуть нас в [в нашем чате](https://t.me/joinchat/RImGNXqbohFkOTg6).
Примерный срок просмотра пулл реквеста до 1000 строк - 24 часа.

Последним шагом является принятие больших благодарностей от нас и разработчиков, которым вы облегчили жизнь :)

## Полезные ссылки
- [Чат поддержки](https://t.me/joinchat/RImGNXqbohFkOTg6)
- [Канал новостей](https://t.me/+-Z63aopFZIw4NDAy)
- [Подробный бэклог](https://st.yandex-team.ru/filters/gantt/order:/all/month/none/Sat%20Jan%2001%202022%2003:00:00%20GMT+0300%20(Moscow%20Standard%20Time)/filter:423575 )
