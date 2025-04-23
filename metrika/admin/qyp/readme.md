## Образы Метрики для QYP

Здесь расположены исходники из которых можно собрать porto-слои и/или образы для VM в QYP

## Как собрать
1. На PR собирается в CI и релизится в testing.
2. На коммит - релиз в CI и релизится в stable.
3. Вручую локально - `ya make -tt ....`
4. Вручную в Sandbox - `YA_MAKE_TGZ`

## Что почитать
[Этушка](https://clubs.at.yandex-team.ru/nirvana/6386/6409#reply-nirvana-6409)

[Образы Infra](https://a.yandex-team.ru/arc/trunk/arcadia/infra/environments/)

## Как вносить изменения
После редактирования файлов, удаления/изменения, нужно обновить файлы `SHA1SUMS`
запустив скрипт `update-digest.sh`, предварительно собрав утилиту
`infra/environments/builder`.
