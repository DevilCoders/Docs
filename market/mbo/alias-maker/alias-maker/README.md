# Alias-maker

Катается по зеленому транку.
Релизная машина: [Alias Maker](https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/alias-maker-arc)


## Devops

### Дашборды

#### Прод

- [JVM и другое](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=alias-maker)
- [alias-maker-meta NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-alias-maker-meta-production)

#### Тестинг

- [alias-maker-meta NGINX](https://solomon.yandex-team.ru/?project=market-mbo&dashboard=mbo-alias-maker-meta-testing)



## Разработка

### Начало работы

Для начала работы сгенерируйте проект с помощью команды

```shell script
ya ide idea --iml-in-project-root --project-root ~/arc/idea-projects/market/mbo/alias-maker
```

и откройте папку проекта в idea.
Данная подходит для структуры каталогов arc, описанной в [wiki](https://wiki.yandex-team.ru/users/sulim/howto/arc-directory-structure/).
Если вы используете другую структуру, замените `~/arc/idea-projects/market/mbo/alias-maker` на нужную папку.

### Сборка и тесты из консоли

Для сборки и запуска тестов из консоли в `ya make` необходимо передать параметр `JDK_VERSION=8`:

```sh
ya make -DJDK_VERSION=8 -ttt .
```

### Локальный запуск

Приложение поддерживает локальный запуск.

1. Для этого нужно один раз настроить компьютер по инструкции: https://wiki.yandex-team.ru/users/s-ermakov/Lokalnyjj-zapusk-s-etcd-datasorsami/#kakzapustit

2. Нужно добавить в конфигурацию запуска в Idea следующие параметры:
    ```
    -Dconfigs.path=${ARCADIA_ROOT}/market/mbo/alias-maker/alias-maker/src/main/properties.d
    -cp
    $Classpath$;${ARCADIA_ROOT}/market/mbo/alias-maker/alias-maker/src/main/conf/local;${ARCADIA_ROOT}/market/mbo/alias-maker/alias-maker/src/main/conf
    ```
3. Скопируйте `11-tokens.properties` в `12-tokens.local.properties` и заполните токены по ссылке.
4. Подсуньте секреты из ya vault (tetsting) `alias-maker.yang.token=`, `alias-maker.yt.token=`, `alias-maker.yql.token=`, `default.oauth.token=`
5. Подсуньте tvm секрет `aliasmaker.auth.tvm.client-secret=`. Ссылку на секрет можно получить в няне в instance spec
6. Скачайте libticket-parser отсюда https://wiki.yandex-team.ru/users/mors741/tvm-ticketparser2java-lib-from-sources/.files/libticketparser2java-2.dylib и подложите в папку dlls (на неё должен указывать конфиг Djava.library.path)
7. Можно запускать локально через Idea Run или Debug запуск.


### Другое

1 этап.

Методы:
getNotMatchedOffers - получить несматченные оферы
checkAliases - проверить кандидаты в алиасы и сохранить их если ок.

Как проверяем алиас:
Считаем статистику матчинга внутри вендора -
сколько сматчено, сколько начало матчиться, сколько изменило матчинг.
Если пороги перейдены - отбрасываем алиас, если нет - сохраняем.

Мы можем только сохранить или пропустить алиас. Удалять старые алиасы не можем.

Проверка качества - смотрим, какие алиасы генерим при Разборе логов на эталонных выборках (для сматченных оферов).

2 этап.

- Удалять старые "плохие" алиасы? что такое "плохие"?
- Генерить алиасы по имени модели - перестановки, переводы, сокращения, синонимы
- Генерация кандидатов в алиасы по оферу, сматченному на модель
- Убирать отформализованные значения прежде чем генерить кандидата на алиас.
- Матчинг м.б. без учета порядка слов (FreeOrderedTokensMatcher и TokensSequenceMatcher)

Допущения 1го этапа:
- Категории без модификаций
- Матчинг только внутри текущего вендора
- Без параметрического матчинга
- Не учитываем блок-слова

### Примечания

- В кэше моделей сейчас храним протобуфки моделей без картиночных параметров и описаний. Картинку оставляем только одну. Это нужно для оптимизации памяти АМ https://st.yandex-team.ru/MARKETIR-8415.
