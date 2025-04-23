# Бэкап GitHub и восстановление репозиториев


{% note warning %}

RO-бэкап всех репозиториев с issues и PR'ами лежит на [gitlab.yandex-team.ru](https://gitlab.yandex-team.ru/groups/yandexclassifieds/-/archived). Выдать доступ новым пользователям **нельзя** - это ограничение гитлаба. 

{% endnote %}

## Общая информация

Бэкап вертикального гитхаба живет в batch-джобе в шиве. Робот идет в гитхаб, собирает информацию о репозиториях в организации. Затем идет через API по https и клонирует зеркало каждого репозитория.
С помощью утилиты restic упаковывает все репозитории и отправляет в s3.

Снапшоты/бэкапы лежат в s3: `s3.mds.yandex.net/vertis-backups/prod/github-backups`

[Карта сервиса](https://a.yandex-team.ru/arc_vcs/classifieds/services/maps/github-backup.yml)
[Манифест деплоя](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy/github-backup.yml)

Исходный код и Dockerfile лежат [тут](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/github-backup)

Необходимые креды [в секретнице](https://yav.yandex-team.ru/secret/sec-01f0e3ptwvs3e1eebnqcxjxay9/explore/versions). Кредами от бэкапа гитхаба мы **не делимся с разработчиками**, т.к. бэкап лежит в бакете `vertis-backups` и заливается/скачивается с соответствующими кредами. Мы не хотим шарить бэкапы на все вертикали.

**Для работы со снапшотами и для восстановления репозиториев необходимо установить утилиту [restic](https://restic.readthedocs.io/en/stable/020_installation.html#macos).**

## Просмотр списка снапшотов

Для просмотра списка снапшотов можно выполнить такой скрипт:
```
#!/bin/bash
export RESTIC_PASSWORD="<restic password из секретницы>"
export RESTIC_REPOSITORY="s3:https://s3.mds.yandex.net/vertis-backups/prod/github-backups"
export AWS_ACCESS_KEY_ID="<AWS_ACCESS_KEY_ID из секретницы>"
export AWS_SECRET_ACCESS_KEY="<AWS_SECRET_ACCESS_KEY из секретницы>"

restic snapshots
```
## Скачивание бэкапов из s3

В начале скрипта так же указываем все необходимые переменные:

```
#!/bin/bash
export RESTIC_PASSWORD="<restic password из секретницы>"
export RESTIC_REPOSITORY="s3:https://s3.mds.yandex.net/vertis-backups/prod/github-backups"
export AWS_ACCESS_KEY_ID="<AWS_ACCESS_KEY_ID из секретницы>"
export AWS_SECRET_ACCESS_KEY="<AWS_SECRET_ACCESS_KEY из секретницы>"
```

Для выкачивания **всех** репозиториев добавляем в конец скрипта команду: `restic restore latest --target <куда скачать все репы локально>`. Опытным путем выяснилось, что выкачивание всех репозиториев на маке в офисе занимает **около часа**.

Для выкачивания **конкретных** репозиториев используем команду: `restic restore latest --target <куда скачать репу> --include github-backups/YandexClassifieds-<reponame>.git`

После выполнения скрипта у вас окажется **mirror** репозитория, а не сам репозиторий. Его необходимо восстановить.

## Востановление репозитория локально

Если есть необходимость восстановить репозиторий локально (без выкачки на github/gitlab/bb/etc), нужно:

1) Изменить название репозитория на его настоящее имя: `mv YandexClassifieds-vertis-packages.git/ vertis-packages.git`
2) Склонировать репозиторий из зеркала: `git clone <полный путь до репозитория .git>`, например: `git clone /Users/mariausova/Desktop/git/restored-vertis-packages/github-backups/vertis-packages.git/`. Обратите внимание, что нужно указывать **полный путь** до репозитория `.git`.

После этого рядом с зеркалом у вас появится сам репозиторий.

## Восстановление репозитория на remote

Есть возможность восстановить репозиторий на любом remote: gitlab/github/bb. Для этого необходимо:
1) На remote создать репозиторий `<repo_name>`;
2) Перейти в mirror `YandexClassifieds--<repo_name>.git`;
3) Указать remote с помощью команды `git remote set-url origin <repo-url>`. `repo-url` можно получить в UI remote'a, нажав на кнопку clone по https. Пример: `git remote set-url origin https://gitlab.cm.expert/sysadmin/restore-backup.git`
4) Выполнить git push.

В ваш репозиторий на remote доедет восстановленный репозиторий.
