# Вазген

Поисковый движок для Вертикальных сервисов

## schema-registry

Смотрит на schema-registry из Аркадии через относительный путь в `build.sbt`, работает из коробки.

## Релиз

#### Локальный запуск

Запускается средствами `IDEA` с
установленным [аркадийным плагином](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij)
и [ya tool](https://wiki.yandex-team.ru/yatool/distrib/). RunConfiguration для каждого из сервисов лежат
в `.run.template`, для запуска переложить в `.run`(но не коммитить туда!). ⚠️ Секреты не коммитить!

###### Внимание!

Начиная с 02.04.2021 для локальной сборки рабочих docker-образов нужно скачать JDK для Linux x86_64.

Сделать это можно скриптом в корне репозитория

```bash
./get-cross-jdk.sh
```

#### Сборка и публикация образов

##### Локально

```
sbt clean
sbt 'vsPlaner/docker:publish'
```

В результате увидим подобное сообщение:

```
[info] Published image registry.yandex.net/vertis/vs-planer:0.2.6-90-90a33c0b
```

Запустить деплой в [`Shiva`](https://admin.vertis.yandex-team.ru/services/vs-planer). В качестве версии указать,
например, `0.2.6-90-90a33c0b`

Номер версии артефакта берется из переменной BUILD_VERSION. Если эта переменная не установлена, номер версии берется из
build.sbt.

### CI

В Tier1 используем TeamCity. Есть tc-джобы:

- [[arc] publish builds](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_Vasgen_PublishArtefactsFromArc&tab=buildTypeStatusDiv&branch_VerticalsBackend_Vasgen=__all_branches__)
    - сборка и публикация образов всех компонент разом.
- [[arc] vs-* для каждой компоненты](https://t.vertis.yandex-team.ru/admin/editBuild.html?id=buildType:VerticalsBackend_Vasgen_ArcVsPlaner)
    - деплой собранных вышеобозначенной джобой компонент на testing.
- [[arc] vs - scalafmt & test](https://t.vertis.yandex-team.ru/admin/editBuild.html?id=buildType:VerticalsBackend_Vasgen_VsArcadia)
    - аналог утраченных github action: проверяет scalafmt и запускает тесты.

Номер версии артефакта берется из переменной **BUILD_VERSION**. В CI **BUILD_VERSION** выставляется с помощью вот такого
скрипта:

```
branch="%teamcity.build.branch%"
branch=`echo "$branch" | grep -o "[0-9]\+"`
if [[ $branch ]]
then
    branch="-$branch"
else
   branch=""
fi
cd classifieds/vs/lib
export BUILD_VERSION=$(date -d `arc log  --max-count 1 $revision classifieds/vs |  grep 'date' | cut -d\  -f2` +\%Y.\%m.\%d.\%H.\%M.\%S$branch | sed 's/[\+/]/-/g')
```

или иными словами - версия равна дате последнего коммита в текущую ветку + номер pr, если ветка отлична от _trunk_.

## Средства мониторинга

### Графики

- [runtime](https://grafana.vertis.yandex-team.ru/d/zGdQawhMk/runtime?&orgId=1)
- [indexer](https://grafana.vertis.yandex-team.ru/d/VUP9YFwnz/indexer?orgId=1)