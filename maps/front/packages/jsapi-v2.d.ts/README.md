# jsapi-v2.d.ts [![build status](https://badger.yandex-team.ru/github/maps/jsapi-v2.d.ts/master/state.svg)](https://github.yandex-team.ru/maps/jsapi-v2.d.ts/commits/master)


[TypeScript](http://www.typescriptlang.org/) definitions for [Maps JS API](https://github.yandex-team.ru/mapsapi/jsapi-v2).

## Installation

1. Install npm package:

```
npm install --registry="http://npm.yandex-team.ru" --save-dev @yandex-int/jsapi-v2-types
```

where `@yandex-int` is internal `Yandex` npm scope.

2. Add `node_modules/@yandex-int/jsapi-v2-types` to `typeRoots` in `tsconfig.json`:

```json
{
    "compilerOptions": {
        "typeRoots": ["node_modules/@yandex-int/jsapi-v2-types"]
    }
}
```

See http://www.typescriptlang.org/docs/handbook/tsconfig-json.html for more information.

## Development

To test definitions run

```
npm test
```

To regenerate `index.d.ts` (e.g., if a new file added) run:

```
npm run gen_index
```

Also note that updated `index.d.ts` should be commited alognside other changes.
