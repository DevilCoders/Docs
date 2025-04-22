# @yandex-fleet/tanker

Node.js [Tanker API](https://doc.yandex-team.ru/Tanker/api-reference/) client.

- [Setup](#setup)
- [Export keyset](#export-keyset)
- [Copy existing key](#copy-existing-key)
- [Copy existing keyset](#copy-existing-keyset)
- [Merge existing keyset](#merge-existing-keyset)
- [Programmatic usage](#programmatic-usage)

## Setup

Add `@yandex-fleet/tanker` to `devDependencies`

```shell
yarn add -D @yandex-fleet/tanker
```

Get your Tanker Token at <https://nda.ya.ru/3SjQY7> and set is as an environment variable

```shell
export TANKER_TOKEN=...
```

## Export keyset

```shell
yarn tanker:export-keyset \
  --project <project> \
  --keyset <keyset> \
  --format <tjson | json>
```

## Copy existing key

```shell
yarn tanker:copy-key \
  --source-key <source-key> \
  --source-project <source-project> \
  --source-keyset <source-keyset> \
  --source-branch <source-project-branch> \
  --destination-key <destination-key> \
  --destination-project <destination-project> \
  --destination-keyset <destination-keyset> \
  --destination-branch <destination-project-branch>
```

## Copy existing keyset

```shell
yarn tanker:copy-keyset \
  --source-project <source-project> \
  --source-keyset <source-keyset> \
  --source-branch <source-project-branch> \
  --destination-project <destination-project> \
  --destination-keyset <destination-keyset> \
  --destination-branch <destination-project-branch>
```

## Merge existing keyset

```shell
yarn tanker:merge-keyset \
  --source-project <source-project> \
  --source-keyset <source-keyset> \
  --source-branch <source-project-branch> \
  --destination-project <destination-project> \
  --destination-keyset <destination-keyset> \
  --destination-branch <destination-project-branch>
```

# Programmatic usage

```ts
import { Tanker } from "@yandex-fleet/tanker";

const tanker = new Tanker({ token: TANKER_TOKEN });

const tjson = await tanker.exportKeysetTJSON({
  project,
  branch,
  keyset,
});
```
