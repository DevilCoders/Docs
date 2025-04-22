# build-kit

Предоставляет готовые инструменты для сборки библиотек

## Установка

```sh
yarn add -D rollup build-kit@workspace:*
```

## Использование

### Аннотируйте package.json

```json
{
    "source": "src/index.ts",
    "main": "dist/index.js",
    "exports": "./dist/index.js",
    "module": "./dist/index.mjs",
    "types": "./dist/index.d.ts",
    "files": ["dist/*"],
    "scripts": {
        "build": "rollup -c",
        "dev": "yarn build --watch"
    }
}
```

### Создайте rollup.config.json

```javascript
import createRollupConfig from 'build-kit';
import packageJson from './package.json';

export default createRollupConfig({
    packageJson,
});
```
