# Transplant history tool arc ⟶ git

## Общее описание

Утилита cli формата для синхронизации истории основной ветки разработки из `arc` в `git` с сохранением топологии.

Идейно утилита делает следующее: проходится по коммитам основной ветки `arc` и переносит их в основую ветку разработки `git` репозитория.
Если утилита встречает `merge commit`, то вместе с `merge commit` она переносит еще и его историю.

Для хранения соответствий `sha` коммитов утилита использует инструмент [git-notes](https://git-scm.com/docs/git-notes). Для каждого коммита,
прозеркалированного в основую ветку разработки в `git`, в `git-notes` заносится соответствующая запись с `msg == <arc commit revision>`. Помимо этого
для каждого коммита проставляются `git-trailers` в commit msg (записи вида `Key: Value`): `Arc-Original-Commit: <arc commit revision>`.
Для всех merge коммитов дополнительно в `trailers` добавляет информацию о RR из которого "получился" merge коммит в `arc`: `Arcanum-Review-Request-Id: <RR id>`.

## Установка

```console
$ npm i @yandex-int/arc-git-transplant-history --registry=https://npm.yandex-team.ru
```

## Требования

* `git` версии `2.29.0` или выше.
* [git lfs] версии `2.7.2` или выше.

[git lfs]: https://wiki.yandex-team.ru/search-interfaces/git-lfs/

## Использование

```сonsole
$ arc-git-transplant-history --help
index.js [OPTIONS]

Tranplant history from arc to git

Arc
      --mount-path    path to arc mount directory            [string] [required]
      --store-path    path to arc store directory            [string] [required]
      --arcadia-path  git repository sync directory in Arcadia
                                                             [string] [required]

Git
  --git-repo-path       git repository cloned directory path [string] [required]
  --git-default-branch  git default branch          [string] [default: "master"]
  --git-notes-ref       git notes sync ref with information of synced arc
                        commits
                     [string] [default: "refs/notes/arc-git-transplant-history"]
  --no-push             no push to git repository after synced histories
                                                      [boolean] [default: false]

Common
  --limit  limit number of commits to sync in main branch
                                                    [number] [default: Infinity]

Options:
  -h, --help     Show help                                             [boolean]
  -v, --version  Show version number                                   [boolean]
```

### Пример

```bash
arc-git-transplant-history  --mount-path /Users/rudeshko/arc/arcadia    \
                            --store-path /Users/rudeshko/arc/store      \
                            --arcadia-path frontend                     \
                            --git-repo-path /Users/rudeshko/frontend/projects/infratest
```

### Пререквизиты использования

⚠ Запись о первом синкнутом моменте истории должна быть сделана вручную! Можно сделать как указано в примере ниже:

```bash
git notes --ref refs/notes/arc-git-transplant-history add HEAD -m "<corresponding arc commit sha in trunk>"
```

* Свежее состояние trunk `arc pull trunk`;
* В `git-repo-path` указать путь на git-репозиторий, где git-хуки отключены и не установлены npm пакеты;
* Путь `mount-path`, `store-path` и `git-repo-path` должны быть абсолютными;
* git-репозиторий склонирован без указания глубины истории (с `--depth N`) и имеет все коммиты.
