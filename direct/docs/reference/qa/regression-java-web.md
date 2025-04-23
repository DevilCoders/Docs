# Регрессия java-Web

Регрессионное тестирование релизов java-Web осуществляется автотестами веб (старого интерфейса и ручек web-api),
а также интеграционными тестами нового интерфейса (b2b и функциональными).

Запуск их в релизах автоматизирован.

Кроме этого на релизном коде должны проходить юнит-тесты.

## Автоматизация { #automation }

### Запуск регрессии веб-интерфейса { #start-web-regression }
[Cron-задача](https://jenkins-direct.qart.yandex-team.ru/job/cron/job/check-if-java-web-release/)
Jenkins дергает по http [ручку](https://radar.qart.yandex-team.ru/radar-rest/onduty/check-if-java-release/?serviceTag=java_web)
в [радаре](../../glossary/glossary.md#radar).
Она:

1. ищет в трекере релиз java-Web в статусе **Можно тестировать**
1. переводит его в статус **Тестируется**
1. создает тикеты на регрессию веб-интерфейса и DNA по шаблонам из MongoDB
1. привязывает их к релизу
1. вызывает Jenkins-задачу
[run_java_release_tests](https://jenkins-direct.qart.yandex-team.ru/job/direct-test-ci/job/run_java_release_tests/),
запускающую [автотесты](#autotests) (список паков захардкожен [тут](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/jenkins-dsl/directci/direct_java_release.groovy))
1. прикладывает в тикет на регрессию веб-интерфейса ссылки на запуски в AQuA

### Запуск регрессии DNA { #start-dna-regression }
{% note info %}

Сейчас автоматический запуск в релизах Web отключен в расчёте на парную сборку релизов Web+DNA.  
Тесты запускаются автоматом только в релизах DNA.

{% endnote %}

По [cron](https://a.yandex-team.ru/search?search=start_dna_tests_in_release_java_web,%5Edirect%2Finfra%2Fdirect-utils%2Fppcdev-scripts-cron%2Fetc%2Fcron.d.*,,arcadia,,5000)'у выполняется скрипт
[start-dna-tests-in-release.py](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/direct-release-tools/bin/start-dna-tests-in-release.py), который:

1. ищет в трекере релиз java-Web в статусе **Можно тестировать** или **Тестируется**
1. ищет привязанный к релизу тикет на регрессию DNA
1. определяет последнюю релизную версию нового интерфейса
1. запускает тесты нового интерфейса в Sandbox
1. прикладывает ссылку на запущеенную задачу в тикет на регрессию DNA
1. дожидается завершения задачи, пишет в тикет результат
1. делает несколько повторных запусков тестов, если были упавшие

{% include [запуск юнит-тестов](_includes/launch-unit-tests.md) %}

## Автотесты { #autotests }

### Веб-интерфейса { #web-autotests }
Паки в акве:

- [Direct Java Web Api](https://aqua.yandex-team.ru/#/pack/591c2e91e4b0457937ed0ce1)

Исходники тестов хранятся в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa).

{% note info %}

Если потребуется удалить тест. Напимер, по причине того, что тесты неактуальны и данный функционал недоступен в интерфейсе. В этом случае необходимо создать тикет и отнести его [Артему](jensenspb@yandex-team.ru)

{% endnote %}


### Интеграционные тесты DNA { #dna-autotests }

Содержит два типа тестов: функциональные и b2b (скриншотами).

Исходники тестов хранятся в [гитхабе](https://github.yandex-team.ru/direct/dna/tree/master/tests).
Есть базовая страничка с [описанием](https://github.yandex-team.ru/direct/dna/blob/master/docs/hermione-tests.md)
и [FAQ](https://wiki.yandex-team.ru/adv-interfaces/direct/faq-testov-dna) на вики.


## Юнит-тесты { #unit-tests }
Юнит-тесты, относящиеся к релизу веб — должны проходить на версии кода, из которой собран релиз.

Простого способа понять, какие модули используются в java-web (чтобы проверить их юнит-тесты) — нет.
Можно отметить следующие модули (от корня `trunk/direct`), код которых используется в Web:
- `core/`
- `libs-internal/core-*`
- `libs-internal/grid*`
- `web/`

Также важны юнит-тесты на соответствие переводов их стабам:
- `I18NBundleCoreTest`
- `I18NBundleCurrencyTest`
- `I18NBundleWebTest`

