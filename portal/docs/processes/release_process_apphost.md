# Релиз Аппхоста (графы)

| NB: Графы релизит только [дежурный Авокадо](https://abc.yandex-team.ru/services/home/duty/?role=3725) |
| ----------------------------------------------------------------------------------------------------- | 

## 1. Выкладка в тестинг
* Для начала нужно убедиться, что нужные коммиты в граф доехали до horizon и корректно импортировались (смотреть на статус ``IMPORTED``). Искать тут [https://horizon.z.yandex-team.ru/revisions](https://horizon.z.yandex-team.ru/revisions)
* Создаем релизный тег
  * Смотрим на список версий, выбираем новую: [https://a.yandex-team.ru/arc/tags/apphost/conf/morda](https://a.yandex-team.ru/arc/tags/apphost/conf/morda)
  * Например ``115-1``
  * Если нужен только тег:
    ```
    svn copy svn+ssh://arcadia.yandex.ru/arc/trunk svn+ssh://arcadia.yandex.ru/arc/tags/apphost/conf/morda/stable-15-1
    ```
  * Чтобы отстрелить новую релизную ветку + релизный тег выполняем две команды. Это может быть нужно, если хочется отстрелить ветку не от trunk'а и, например, cherry-pick'нуть коммиты:
    ```
    svn copy svn+ssh://arcadia.yandex.ru/arc/trunk svn+ssh://arcadia.yandex.ru/arc/branches/apphost/conf/morda/stable-15
    ```
    ```
    svn copy svn+ssh://arcadia.yandex.ru/arc/branches/apphost/conf/morda/stable-15 svn+ssh://arcadia.yandex.ru/arc/tags/apphost/conf/morda/stable-15-1
    ```
* Клонируем задачу [https://sandbox.yandex-team.ru/task/945583040/](https://sandbox.yandex-team.ru/task/945583040/) с указанием новой версии ``stable-15-1``
* Далее надо дождаться валидации своего тега на странице [https://horizon.z.yandex-team.ru/tags?vertical=MORDA](https://horizon.z.yandex-team.ru/tags?vertical=MORDA)
* В созданной задаче после выполнения нажать `release` => `testing`
* Проверить, что testing-аппхост корректно выкатился:
  * Морда [testing-portal-apphost](https://nanny.yandex-team.ru/ui/#/services/catalog/testing-portal-apphost/)
  * avocado/geohelper - [testing-avocado-apphost](https://nanny.yandex-team.ru/ui/#/services/catalog/testing-avocado-apphost/)
* Запустить автотесты на морду. Тесты нужно нацелить на тестинг - https://rc.yandex.ru
  * [hermione](https://teamcity.yandex-team.ru/buildConfiguration/PortalAkaMordaProjects_PortalMordaXenial_PortalMordaAutotestingRc)
  * [cypress](https://teamcity.yandex-team.ru/buildConfiguration/PortalAkaMordaProjects_PortalMordaXenial_PortalMordaAutotestingCypress)
  * [api search](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_ApiSearchTests)
  * [api yabrowser 2](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_ApiYabrowser2)
  * [cleanvars](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_Cleanvars)
  * [schema tests simple](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_SchemaTestsSimple)


## 2. Выкладка в продакшн
* Убедиться, что в тестах нет новых, неожиданных или необъяснимых ошибок
* Далее в задаче продолжить релиз `release` => `stable`
* Дальше выкатывать через дашборд
  - Дашборд для морды - [morda_apphost](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/morda_apphost/)
    Для выкладки надо использовать рецепт morda-apphost

  - Дашборд avocado/geohelper - [avocado](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/avocado/)


{% note warning %}

Не нужно коммитить и катить бинари аппхоста, даже если они на дашборде есть. Релизами бинарей занимается команда аппхоста.

{% endnote %}
