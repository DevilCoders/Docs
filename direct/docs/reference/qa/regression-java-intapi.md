# Регрессия java-Intapi

Регрессионное тестирование релизов java-Intapi осуществляется автотестами.

Запуск их в релизах автоматизирован.  
Также есть автоматический перезапуск тестов (пока недокументирован).


## Автоматизация { #automation }

### Запуск регресси intapi { #start-intapi-regression }
[Cron-задача](https://jenkins-direct.qart.yandex-team.ru/job/cron/job/check-if-java-intapi-release/)
Jenkins дергает по http [ручку](https://radar.qart.yandex-team.ru/radar-rest/onduty/check-if-java-release/?serviceTag=java_intapi)
в [радаре](../../glossary/glossary.md#radar).
Она:

1. ищет в трекере релиз java-Intapi в статусе **Можно тестировать**
1. переводит его в статус **Тестируется**
1. создает тикет на регрессию по шаблону из MongoDB
1. привязывает его к релизу
1. вызывает Jenkins-задачу
[run_java_release_tests](https://jenkins-direct.qart.yandex-team.ru/job/direct-test-ci/job/run_java_release_tests/),
запускающую [автотесты](#autotests) (список паков захардкожен [тут](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/jenkins-dsl/directci/direct_java_release.groovy))
1. прикладывает в тикет на регрессию ссылки на запуски в AQuA

{% include [запуск юнит-тестов](_includes/launch-unit-tests.md) %}

## Автотесты { #autotests }
Паки в акве:

- [directweb: save with java-intapi pack](https://aqua.yandex-team.ru/#/pack/5d974bbf8a900e039444043b)
- [direct java intapi](https://aqua.yandex-team.ru/#/pack/58526ca6e4b04506a0ac2172)

Исходники тестов хранятся в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa).

## Юнит-тесты { #unit-tests }
Юнит-тесты, относящиеся к релизу интапи — должны проходить на версии кода, из которой собран релиз.

Обязательно должны проходить юнит-тесты самого intapi (в модуле приложения).
Кроме них следует проверять тесты модулей, используемых в java-intapi, но нет простого способа понять их список.

Также важны юнит-тесты на соответствие переводов их стабам:
- `I18NBundleCoreTest`
- `I18NBundleCurrencyTest`
- `I18NBundleIntapiTest`
