@yandex-lego/gh-gap
--------------------

Утилита, определяющая список измененных пакетов на основе списка измененных файлов в PR.
Предназначена для использования там, где нет доступа к файловой системе.
Измененные пакеты определяет на основе сопоставления путей до измененных файлов со списком пакетов `lerna.json`.

`affectedPaths = await getAffectedPackages({ owner, repo, number, cached });`