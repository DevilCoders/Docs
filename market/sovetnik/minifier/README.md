# Minifier

This repo is only for moderators from browser stores.

## How to prepare scripts for moderation

View our [wiki page](https://wiki.yandex-team.ru/sovetnik/webstores/process-obnovlenija-rasshirenija-v-veb-storax/)

## How to debug changes in this package

The best way to do it is via [npm link](https://docs.npmjs.com/cli/link). It will create a global symlink to this folder.

1. In _sovetnik-minifier_ repo execute:

```sh
npm link
```

1. Go to _static repo_ and execute the following command:

```sh
npm link sovetnik-minifier
```

3. Make changes

4. In _static repo_ run:

```sh
grunt sovetnik-extension # create build folder with all extensions
npm run minifier:copy # copy sovetnik-minifier from node_modules to dist folder in the project root
npm run minifier:run # run minifier tests
```

to check that minifier tests are passing.

5. Delete global symlink:

```sh
npm un sovetnik-minifier && npm install # in static repo
npm un # in sovetnik-minifier repo
```
