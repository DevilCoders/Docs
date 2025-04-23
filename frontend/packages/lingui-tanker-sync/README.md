# lingui-tanker-sync

Утилита для синхронизации переводов в формате Lingui-js с Танкером

## Lib usage
```js
const { upload, download } = require('lingui-tanker-sync');

download({
    dir: './locale',
    project: 'lingui',
    keyset: 'lingui',
    branch: 'lingui'
})
    .then(() => console.log('Finished'))
    .catch(err => console.error(err));

upload({
    dir: './locale',
    project: 'lingui',
    keyset: 'lingui',
    branch: 'lingui'
})
    .then(() => console.log('Finished'))
    .catch(err => console.error(err));

```

## CLI usage
```bash
./cli.js upload -d ./locale -p projectname -k keysetname -b branchname -a auth_token
./cli.js download -d ./locale -p projectname -k keysetname
```

```
./cli --help

Usage: ./cli.js download -p projectId -k keyset -d dir [-b branchName]
Usage: ./cli.js upload -p projectId -k keyset -d dir -l default locale [-b branchName]

Options:
  --version      Show version number     [boolean]
  --dir, -d      Target directory        [string] [required]
  --project, -p  Tanker project id       [string] [required]
  --keyset, -k   Tanker keyset id        [string] [required]
  --token, -a    Tanker OAuth token      [string]
  --branch, -b   Tanker branch name      [string] [default: "master"]
  --locale, -l   Default locale          [string] [required] [default: "ru"]
  --help         Show help               [boolean]

```

[![Build Status](https://drone.yandex-team.ru/api/badges/toolbox/lingui-tanker-sync/status.svg)](https://drone.yandex-team.ru/toolbox/lingui-tanker-sync)
