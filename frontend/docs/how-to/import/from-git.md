# Иммиграция git-репозитория

Руководство описывает миграцию git-репозитория в монорепозиторий frontend с сохранением истории изменений.

> ⚠️ Перед заездом необходимо убедиться что мигрирующий репозиторий удовлетворяет [требованиям][requirements].

[requirements]: ../../faq/requirements.md

## Подготовка

Для удобства выполнения следующих шагов, в текущей сессии терминала объявите следующие переменные окружения:

* `GITHUB_OWNER` — Имя владельца репозитория или организации.
* `GITHUB_REPO` — Название репозитория.
* `PACKAGE_NAME` — Желаемое название будущей директории внутри `packages` или `services`, в которую иммигрирует репозиторий. Хорошее значение по умолчанию: `$GITHUB_OWNER-$GITHUB_REPO`.

Например, для репозитория `https://github.yandex-team.ru/paskills/store`:

```shell
export GITHUB_OWNER=paskills
export GITHUB_REPO=store
export PACKAGE_NAME=$GITHUB_OWNER-$GITHUB_REPO # paskills-store
```

Также убедитесь, что ваш логин в переменной окружения `$USER` совпадает с логином на GitHub.

### Заморозка разработки

Перейдите в настройки вашего репозитория на GitHub и [заархивируйте][gh-archive] его, нажав кнопку **Archive this repository**.

```shell
open https://github.yandex-team.ru/$GITHUB_OWNER/$GITHUB_REPO/settings#danger-zone
```

После указанных действий влитие изменений в основную ветвь разработки будет запрещено.

[gh-archive]: https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/archiving-repositories

### Форк монорепозитория

Создайте _личный_ форк монорепозитория на GitHub:

```shell
open https://github.yandex-team.ru/search-interfaces/frontend/fork
```

Он понадобится для отправки пулл-реквеста с историей мигрирующего репозитория.
Дальнейшие шаги подразумевают, что личный форк расположен по следующей ссылке:

```
https://github.yandex-team.ru/$USER/frontend
```

Также потребуется [добавить][add-collab] [@robot-merge-queue] в **Collaborators** созданного форка:

```shell
open https://github.yandex-team.ru/$USER/frontend/settings/access
```

См. [документацию][mq-readme] сервиса Merge Queue.

> 🔄 Если личный форк уже есть, убедитесь что его основная ветка не сильно отстала от исходного монорепозитория.

[@robot-merge-queue]: https://github.yandex-team.ru/robot-merge-queue
[add-collab]: https://docs.github.com/en/github/setting-up-and-managing-your-github-user-account/inviting-collaborators-to-a-personal-repository
[mq-readme]: https://github.yandex-team.ru/search-interfaces/microservices/blob/master/services/merge-queue/README.md

### Координация

[Уведомите][infraduty-form] команду инфраструктуры, призовите [@blond] и [@sipayrt].
Будет создан INFRADUTY-тикет.

[infraduty-form]: https://wiki.yandex-team.ru/infraduty/form/
[@blond]: https://staff.yandex-team.ru/blond
[@sipayrt]: https://staff.yandex-team.ru/sipayrt

## Миграция

### Подготовка рабочих копий

Создайте временную рабочую директорию для импорта:

```shell
export IMPORT_WORKDIR=$(mktemp -d /tmp/frontend-import-$PACKAGE_NAME.XXXX)
```

> Здесь `XXXX` — плейсхолдер, используемый [`mktemp`][https://linux.die.net/man/1/mktemp].

Склонируйте в рабочую директорию монорепозиторий из личного форка, добавьте исходный монорепозиторий в качестве ремоута:

```shell
cd $IMPORT_WORKDIR
git clone git@github.yandex-team.ru:$USER/frontend.git

cd frontend
git remote add upstream git://github.yandex-team.ru/search-interfaces/frontend.git
git pull upstream master
git checkout -b import/$PACKAGE_NAME
```

Подготовьте рабочую копию мигрирующего репозитория.

```shell
cd $IMPORT_WORKDIR
git clone --single-branch --no-tags git@github.yandex-team.ru:$GITHUB_OWNER/$GITHUB_REPO.git $PACKAGE_NAME
cd $PACKAGE_NAME
```

### [Git LFS]

> Этот шаг можно пропустить, если в вашем репозитории только текстовые файлы — нет картинок, шрифтов, макетов, баз данных, архивов, скомпилированных библиотек и им подобных.

Чаще всего в LFS необходимо конвертировать только скриншоты и тестовые данные [Hermione], маски которых описаны в файле [`.gitattributes`][gitattributes] в корне монорепозитория:

[gitattributes]: ../../../.gitattributes
[Hermione]: https://github.com/gemini-testing/hermione

```
**/test-data/**/*.gz
**/screens/**/*.png
```

Однако, есть шанс случайно привнести в историю монорепозитория что-то лишнее и замедлить разработку через `git`.
Для исключения неприятных сюрпризов оценку объёма стоит сделать в любом случае.

#### Оценка размера репозитория

Установите необходимые утилиты через [`brew`][brew]:

```shell
brew update
brew install git-lfs gnu-sed
```

Настройте Git LFS:

```shell
git config --global filter.lfs.process "git-lfs filter-process --skip"
git config --global filter.lfs.smudge "git-lfs smudge --skip %f"
git config --global filter.lfs.clean "git-lfs clean %f"
git config --global lfs.https://github.yandex-team.ru/.locksverify false
```

> ❗️ Если что-то пошло не так, попробуйте найти ответ в [сборнике решений][git-lfs-doc] по работе с Git LFS.

Выполните в корне репозитория следующие команды:

```shell
git gc
git count-objects --verbose --human-readable
git bundle create tmp.bundle --all; du -h tmp.bundle; rm tmp.bundle
git lfs migrate info --include-ref=$(git symbolic-ref refs/remotes/origin/HEAD)
```

Получите список бинарных файлов ([объяснение команды][git-find-binary]):

```shell
git log --all --numstat --oneline | grep '^-' | cut -f3 | gsed -r 's|(.*)\{(.*) => (.*)\}(.*)|\1\2\4\n\1\3\4|g' | sort -u
```

Вывод команд опубликуйте на [Paste] и приложите в INFRADUTY-тикет.

#### Конвертация

На основе списка бинарных файлов в репозитории подберите подходящие маски путей и конвертируйте бинарные файлы в LFS.
Например:

```shell
git lfs migrate import --everything --include="**/*.png,**/*.gz"
```

Очистите `.git` от мигрировавших файлов:

```shell
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

Снова выполните команды для подсчёта размера репозитория и приложите в INFRADUTY-тикет.

[Git LFS]: https://git-lfs.github.com/
[brew]: https://brew.sh/
[git-lfs-doc]: https://wiki.yandex-team.ru/search-interfaces/git-lfs/
[git-find-binary]: https://stackoverflow.com/a/42705051
[Paste]: https://paste.yandex-team.ru/

### Миграция истории

Запустите команду `lerna import` для миграции истории в монорепозиторий:

```shell
cd ../frontend

# Для пакета укажите --dest packages
npx lerna import ../$PACKAGE_NAME/ --dest packages --preserve-commit

# Для сервиса укажите --dest services
npx lerna import ../$PACKAGE_NAME/ --dest services --preserve-commit
```

Если история мигрирующего репозитория нелинейна, команда завершится с ошибкой конфликта.

Можно воспользоваться опцией [`--flatten`][lerna-flatten].
Это снизит риск конфликтов, так как при миграции merge-коммиты будут заменены на squash-коммиты.

```shell
# Для пакета укажите --dest packages
npx lerna import ../$PACKAGE_NAME/ --dest packages --preserve-commit --flatten

# Для сервиса укажите --dest services
npx lerna import ../$PACKAGE_NAME/ --dest services --preserve-commit --flatten
```

> При замене merge-коммитов на squash-коммиты теряется детализация.
> Вместо нескольких коммитов внутри merge-коммита в истории монорепозитория будет сохранён один коммит, содержащий их изменения.

Чтобы сохранить детализацию, нужно привести историю к линейному виду.

[lerna-flatten]: https://github.com/lerna/lerna/tree/main/commands/import#--flatten

#### Линеаризация истории

![vcs-linear-history](../../images/vcs-linear-history.png)

Получите рабочую копию git-репозитория:

```shell
git clone git@github.yandex-team.ru:$GITHUB_OWNER/$GITHUB_REPO.git

cd $GITHUB_REPO
```

Выполните `rebase` по первому коммиту в репозитории:

```shell
git rev-list --max-parents=0 HEAD | xargs git rebase --strategy-option theirs
```

##### Конфликты при линеаризации истории

После выполнения команды могут возникнуть конфликты с одновременным добавлением, удалением или изменением файлов: `DD`/`AA`, `AU`/`UA`, `DU`/`UD`.

> Подробнее о стратегии `theirs` читайте в [документации][git-adv-merge] к `git`.

Чтобы разрешить конфликт вручную, соблюдая стратегию `theirs`, нужно делать либо `git add`, либо `git rm`, в зависимости от того, на чьей стороне было изменение.

Можно воспользоваться скриптом [`rebase-continue`][rebase-continue] для разрешения конфликтов.
Выполняйте следующие команды, пока конфликты не закончатся:

```shell
node rebase-continue.js
git rebase --continue
```

После нужно компенсировать тот `diff`, получившийся в процессе разрешения конфликтов:

```shell
git diff --unified --patch master origin/master | git apply
git commit --all --message="sync history"
``` 

[git-adv-merge]: https://git-scm.com/book/ru/v2/Инструменты-Git-Продвинутое-слияние
[rebase-continue]: https://paste.yandex-team.ru/2363876/text

#### Отправка истории в монорепозиторий

Отправьте коммиты с историей в личный форк:

```shell
git push origin import/$PACKAGE_NAME
```

Создайте пулл-реквест в монорепозиторий `frontend`:

```shell
open https://github.yandex-team.ru/search-interfaces/frontend/compare/master...blond:import/$PACKAGE_NAME
```

#### После миграции

Проставьте первый тег для сервиса (так как релизная машинерия пока завязана на гите, то все действия нужно проводить в нём):

* узнайте на какой коммит и какой тег ставить, формат тега можно посмотреть в конфиге, чаще всего это {service-name}/v{версия} (за версию нужно брать версию из package.json на момент миграции или ставить v1.0.0);
* поставьте тег (`git tag -a <tagname> <commit>`);
* пушните тег (`git push --tags`).
