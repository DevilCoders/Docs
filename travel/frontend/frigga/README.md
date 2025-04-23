# Frigga

[![npm version](https://badger.yandex-team.ru/npm/@yandex-data-ui/frigga/version.svg)](https://npm.yandex-team.ru/@yandex-data-ui/frigga)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/frigga&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/frigga)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/frigga&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/frigga)
[![distribution health](https://badger.yandex-team.ru/oko/pkg/@yandex-data-ui/frigga/health.svg)](https://oko.yandex-team.ru/pkg/@yandex-data-ui/frigga)

Generates react-component icons from Figma file via [Figma API](https://www.figma.com/developers/api).

## Install

```
npm i @yandex-data-ui/frigga --save-dev
```

## How to get **file key**

Open page with icons in Figma. Url of this page contains **key**
www&#46;figma&#46;com/file/**{key}**/your.project?node-id=**{id}**

## How to get and set Figma auth token

[Instruction](https://www.figma.com/developers/api#access-tokens)

and pass via CLI param

```
frigga -t '<token>'
```

or set env variable

```
FIGMA_AUTH_TOKEN=<token>
```

---

## Rules for icons in Figma files

-   All icons should be defined as [components](https://help.figma.com/article/66-components)
-   Each icon component must have an unique name
    -   Icon can have slashes in name: `12 / Ok` and `16 / Ok`. This can help to organize icons
-   Is is possible to select components for exporting using the [select](#select) option

## Configuration

Create config file and pass config file path via CLI param --config or -c.

```
frigga -c './examples/ya-travel.typescript.frigga.config.ts'
```

-   [Example configuration TS](./examples/ya-travel.typescript.frigga.config.ts)
-   [Example configuration JS](./examples/ya-travel.javascript.frigga.config.js)

### FriggaOptions

-   Config file: [IFriggaOptions](./src/types/IFriggaOptions.ts)
-   CLI params: [yargs.options](./src/cli/cli.ts)

In case of parameter conflict, config file has priority on CLI params.

### select

`select({name, key}: {name: string, key: string}): boolean` — if method returns false
component would be skipped.

### getFileName

`getFileName({name, key}: {name: string, key: string}): string` - defines the
exported icon filename. Filename can contain slashes to make nested directory structure,
for example: `12/Ok.js` would create file `Ok.js` in folder `12`.

### getComponentName

`getFileName({name, key}: {name: string, key: string}): string` - defines the
component name of the exported icon. Must be valid variable name.

### getSvgrConfig

`getSvgrConfig({name, key}: {name: string, key: string}): object` - defines the
[svgr configuration](https://github.com/gregberge/svgr/blob/main/packages/core/src/config.ts)
which would be used for icon processing and component generation.

### Raster images

For sync raster images view example [example](./examples/ya-travel.png.typescript.frigga.config.ts)

## TypeScript

To generate components in TypeScript, add property `typescript: true` in config from [getSvgrConfig](#getsvgrconfig)
with typescript icon template. [Example](./examples/ya-travel.typescript.frigga.config.ts).

## How it looks like

![demo](./demo.gif)

## Known issue

```
node_modules/@types/istanbul-reports/index.d.ts:8:16 - error TS2305: Module '"istanbul-lib-report"' has no exported member 'ReportBase'.
```

### Solution

```
npm i --save-dev @types/istanbul-lib-report
```

Delete `./node_modules/@types/istanbul-reports/node_modules/@types/istanbul-lib-report`, because it is an old version.

The idea is: install latest version, manually find and delete old version.
