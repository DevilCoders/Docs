# jenkins-dsl
dsl скрипты для генерации сборок в дженкинсе </br>
https://github.com/jenkinsci/job-dsl-plugin/wiki

## directci
Генерация джоб для сборки артефактов с интеграционными автотестами

Настройка сборки артефактов с тестами (и сопутствующих) осуществляется в 
directci/config.yml

Дефолтный билдер умеет собирать проекты из https://github.yandex-team.ru/direct-qa
ключ сборки в конфиге должен совпадать с именем репозитория.

Основные параметры
<ul>
<li>enabled. Джоба создается активной, если параметр задан как true, в противном случае - неактивной</li>
<li>version. Версия, с котрой надо собирать артефакт</li>
<li>skip. Не создавать джобу, если true</li>
<li>email. Электронные адрес для получения нотификаций. Если не задан, direct-autotests-notifications@yandex-team.ru</li>
<li>downstream. Список сборок, которые нужно запустить при успешной сборке. Есть возможность передать в них значение MVN_GOAL, указав ее в goal. Сборки тригерятся только в случае, если VERSION во время сборки совпадает с дефолтной версией  (дефолтная версия = или 1.0-SNAPSHOT или указанная в config.yml)</li>
<li>builderClass. Для кастомной сборки можно указать класс сборщика из directci/builders. Например, как directci/DirectDbModels.groovy</li>
</ul>

Для перегенарации джоб надо выполнить:
https://jenkins-direct.qart.yandex-team.ru/job/dsl/job/direct-qa-ci-up/
