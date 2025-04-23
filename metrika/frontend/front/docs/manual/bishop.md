# Про Bishop

Официальная [дока](https://docs.yandex-team.ru/bishop/).

[Bishop](https://bishop.mtrs.yandex-team.ru/) — система для создания и управления конфигурациями.

Мы используем его для конфигурирования:
— Флагов фичей (когда функциональность скрываем за флаг)
— Настроек api (хост, таймаут, ретраи)
— Настроек TVM
— Настроек подключения к монге
— Конфигов сервисов (blackbox, passport, mds)
— И др.

## Окружения

Мы используем три основных окружения (стейбл, престейбл, тестинг) + окружения, которые заводим для автобет.

### Для бэм-метрики:

* [Stable](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika-bem)
* [Pre-Stable](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika-bem.prestable)
* [Testing](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika-bem.testing)

### Для react-метрики

* [Stable](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika)
* [Pre-Stable](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika.prestable)
* [Testing](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika.testing)

Конфиги Testing и Pre-Stable наследуют свои конфиги от Stable конфига, целесообразно начинать добавления новых значений с родительского конфига.

# Примеры

## Добавление нового окружения

1. Выбираем окружение, от которого будем наследоваться. Для примера, возьмем [metrika.deploy.frontend.metrika.testing.development](https://bishop.mtrs.yandex-team.ru/environment/metrika.deploy.frontend.metrika.testing.development)
2. Клонируем окружение с помощью кнопки `Clone` в шапке
![clone](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-01T19%3A33%3A44.192517.jpg)

В форме указываем название нового окружения и родительское окружение и сохраняем по кнопке `Submit`
![clone-form](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-01T19%3A35%3A02.479572.jpg)

3. Далее, привязываем к окружению конфиг. Переходим в родительское окружение, в левом меню на вкладку `Configs`.
   В появившейся таблице конфигов кликаем по ссылке в `Program`
![config-tab](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-01T19%3A39%3A13.411305.jpg)

4. В выбранной программе жмем кнопку `Attach environment`, выбираем ранее созданное окружение и сохраняем по кнопке `Submit`
![attach-env](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-01T19%3A42%3A00.673544.jpg)
![attach-form](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-01T19%3A43%3A46.824323.jpg)

## Привязка окружения к стенду

1. Переходим в deploy, выбираем нужный нам stage. Например, автобету:
`https://deploy.yandex-team.ru/stages/<Stage Name>`

2. Переходим на вкладку `Config`
![deploy-config](https://jing.yandex-team.ru/files/gakuznetsov/uhura_2021-10-01T19%3A51%3A00.227633.jpg)

Для изменения окружения BEM-метрики переходим в `BEM-workload`
Для изменения окружения React-метрики переходим в `EXPRESS-workload`

Нажимаем кнопку `Edit` и в разделе `Environment variables` находим `BISHOP_ENVIRONMENT_NAME` и подменяем `Value` на новое окружение.
Нажимаем в модалке `Apply`, затем в шапке `Update` и деплоим изменения.

Если автобета будет пересобираться (например, после коммита в ветку), то изменения конфига слетят на дефолтные.

## Добавление нового значения в features

В окружении, в таблице с конфигом в столбце `Relation` могут быть значения:
* `INHERITED` — конфиг наследуется от родителя
* `Local` — родительский конфиг переопределен

Чтобы переопределить конфиг, в нужной строке справа нужно кликнуть на троеточку и выбрать `Override`.
В модалке добавить необходимое значение, и нажать кнопку `Submit`.

Рекомендуется добавлять фичи, которые по дефолту скрыты, например: `isSomeFeatureShown: true | false`. В обратном случае, если по каким-то причинам переменная не будет выставлена, есть риск, что пользователи увидят то, что не должны.
