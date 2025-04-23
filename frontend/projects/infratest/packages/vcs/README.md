# @yandex-int/vcs

Слой абстракции над VCS: git, arc.

## Использование

```typescript
import { createVcs } from "@yandex-int/vcs";

const rootPath = process.cwd();

// Вторым аргументом можно указать путь до конфигурационного файла.
// По умолчанию – `${rootPath}/.config/vcs.json`
const vcs = createVcs(rootPath);

// Вернёт абсолютный путь до репо. В аркануме – с добавлением пути поддиректории (см. конфигурацию).
await vcs.getTopLevel();

// Синхронный интерфейс
vcs.getTopLevelSync();

// Вернёт список всех изменённых файлов (`{ type: FileChangeType, path: string }`) относительно "top level" директории.
// Пути указываются относительно `rootPath`.
await vcs.getChangedFiles({ paths: ["./packages"], from: "arcadia/trunk", to: "HEAD" });

// Вернёт список изменений в локальной ветке относительно ветки "arcadia/trunk", синхронно.
vcs.getChangedFilesSync({
    paths: ["./"],
    from: vcs.getMergeBaseSync({ commitA: vcs.trunk, commitB: "HEAD" }),
    to: "HEAD",
});
```

## Конфигурация

По умолчанию используется конфиг из `${rootPath}/.config/vcs.json`. Формат:

```typescript
export type VcsConfig = {
    arcadia?: {
        // Опциональный путь поддиректории. Например, "frontend/projects/infratest/". Слеш на конце имеет значение.
        path?: string;
        // По умолчанию "arcadia/trunk".
        trunk?: string;
    };
    git?: {
        // По умолчанию "origin/master".
        trunk?: string;
    };
};
```
