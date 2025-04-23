# Регрессия perl

Регрессионное тестирование релизов perl осуществляется автотестами.

Запуск их в релизах автоматизирован.
Также есть автоматический перезапуск тестов (пока недокументирован).


## Автоматизация { #automation }

### Запуск регресси perl { #start-perl-regression }
[Cron-задача](https://jenkins-direct.qart.yandex-team.ru/job/cron/job/check-if-release/)
Jenkins дергает по http [ручку](https://radar.qart.yandex-team.ru/radar-rest/onduty/check-if-release/)
в [радаре](../../glossary/glossary.md#radar).
Она:

1. ищет в трекере релиз perl в статусе **Можно тестировать**
1. переводит его в статус **Тестируется**
1. создает тикеты на регрессию по шаблону из MongoDB
1. привязывает их к релизу
1. вызывает Jenkins-задачу
   [run_release_tests](https://jenkins-direct.qart.yandex-team.ru/job/direct-test-ci/job/run_release_tests/),
   запускающую [автотесты](#autotests) (список паков захардкожен [тут](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa/jenkins-dsl/directci/direct_release.groovy))
1. прикладывает в тикет на регрессию ссылки на запуски в AQuA

Отдельно создаются 3 тикета на регрессию:

1. cmd [Пример](https://st.yandex-team.ru/DIRECT-143624)
1. INTAPI, Транспорт БК, Транспорт в Модерацию [Пример](https://st.yandex-team.ru/DIRECT-143625)
1. API [Пример](https://st.yandex-team.ru/DIRECT-143626)

{% include [запуск юнит-тестов](_includes/launch-unit-tests.md) %}

## Автотесты { #autotests }
Список паков в акве можно найти в примерах тикетах на регрессию.

Исходники тестов хранятся в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/qa).

Инструкции по локальной сборке и запуску находятся [здесь](https://wiki.yandex-team.ru/users/upcfrost/avtotesty-direkta-posle-pereezda-v-arkadiju/#razrabotka) и [здесь](https://st.yandex-team.ru/DIRECTKNOL-55).

Удобным способом просмотра упавших тестов по тегу является скрипт `direct-check-release-in-aqua.pl`. Запускаем его на `ppcdev`.<br> 
Скрипт по захардкоженному набору названий лончей и дате релиза идет в Акву и провеяет, что все паки были запущены. Для запущенных паков выводит тесты, которые не прошли хотя бы в одном из запусков. Набор лончей задается профилем; при запуске сприпта можно выбрать, в каком профиле работаем.
Команда для запуска выглядит так:

`direct-check-release-in-aqua.pl -p [профиль] -t [тэг]`<br>

где

`-p|--profile` - профиль (задает набор лончей с которыми работаем) для перла может принимать значения:
- `cmd` - тесты регрессии `cmd`
- `intapi` - тесты `INTAPI` регрессии внутреннего API и транспорта
- `transport` - тесты транспорта в БК и Модерацию регрессии внутреннего api и транспорта
- `api` - тесты регрессии внешнего API
- `perl_regression_duty` - тесты всех регрессий перла сразу.

`-t|--tag` - полное название тега запуска в Акве<br>

Примеры запуска:<br>
1. Показать все упавшие автотесты перла в релизе с тегом `direct-release-perl-DIRECT-162414-2022-02-07`
    ```
    direct-check-release-in-aqua.pl -p perl_regression_duty -t direct-release-perl-DIRECT-162414-2022-02-07
    ```
2. Показать все упавшие автотесты транспорта перла в релизе с тегом `direct-release-perl-DIRECT-162414-2022-02-07`
    ```
    direct-check-release-in-aqua.pl -p transport -t direct-release-perl-DIRECT-162414-2022-02-07
    ```
3. Показать статистику по всем упавшим автотестам перла в релизе с тегом `direct-release-perl-DIRECT-162414-2022-02-07`
    ```
    direct-check-release-in-aqua.pl -p perl_regression_duty -t direct-release-perl-DIRECT-162414-2022-02-07 --brief --sh | sort -nr
    ```

Как исправить некоторые ошибки, возникающие в регрессиях перла [можно посмотреть тут](../../guide/troubleshooting/perl-regression-errors.md).

## Юнит-тесты { #unit-tests }
Юнит-тесты, относящиеся к релизу perl — должны проходить на версии кода, из которой собран релиз.

Обязательно должны проходить юнит-тесты самого perl (в модуле приложения).
Кроме них следует проверять тесты модулей, используемых в perl, но нет простого способа понять их список.
