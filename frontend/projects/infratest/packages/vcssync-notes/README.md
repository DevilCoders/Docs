# vcssync-notes

[VCS Sync] - инструмент для синхронизации git проектов из GitHib в Аркадию. В настройках проекта в GitHub настраивается вебхук, и сервис все новые коммиты из master/dev ветки переносит в Аркадию. При этом LFS файлы раскрываются и превращаются в бинарные.

Для внутренней машинерии VCS Sync использует [git notes]. Маппинг `git коммиты → svn ревизии` хранится в git notes.

Посмотреть svn ревизию по хэшу git коммита можно так:

```console
git init vcssync-notes

cd vcssync-notes

git remote add origin git@github.yandex-team.ru:serp/web4.git
git fetch origin refs/notes/vcssync:refs/notes/vcssync

# Посмотреть notes на конкретный коммит
git notes --ref refs/notes/vcssync show <COMMIT_HASH>
```

Пакет инкапсулирует вышеописанную логику и предоставляет абстракцию для поиска ревизию по хэшу git коммита.

[VCS Sync]: https://wiki.yandex-team.ru/repo/vcs-sync/devops/
[git notes]: https://git-scm.com/docs/git-notes

## Установка

```console
npm i @yandex-int/si.ci.vcssync-notes --registry=https://npm.yandex-team.ru
```

## Требования

Для корректной работы требуется, чтобы в PATH был определен путь до исполняемого файла git.

## Использование

```ts
import { VcsSync } from "@yandex-int/si.ci.vcssync-notes";

const vcsSync = new VcsSync("git@github.yandex-team.ru:serp/web4.git");

// Получить ревизию коммита в Аркадии по хэшу git коммита.
await vcsSync.getSvnRevisionByGitCommitHash(commitHash);

// Получить ревизию коммита в Аркадии по хэшу git коммита с ретраями.
await vcsSync.getSvnRevisionByGitCommitHashWithRetry(commitHash);

// Получить ревизию коммита в Аркадии по имени remote ветки.
await vcsSync.getSvnRevisionByGitRemoteBranch(branch);
```
