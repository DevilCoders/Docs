# @yandex-market/mbo-model-title

## Установка

```bash
npm install ramda @yandex-market/market-proto-dts @yandex-market/mbo-parameter-editor
npm install @yandex-market/mbo-model-title
```

## Сборка

```bash
npm run build
```

## Запуск тестов

```bash
npm run test
```

## Codestyle

```bash
npm run lint
```

## Использование

```typescript
import { createTitleGenerator, ModelTitle } from '@yandex-market/mbo-model-title';

const titleGenerator = createTitleGenerator(categoryData);

const modelTitle: ModelTitle = titleGenerator.createModelTitle({ titleTemplate: '[true, t0]', model });
const skuTitle: ModelTitle = titleGenerator.createSkuTitle({ titleTemplate: '[true, t0]', model });
```
