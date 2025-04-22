# @yandex-market/market-proto-dts

Данный пакет содержит типы сгенерированные на основе protobuf из репозитория [https://github.yandex-team.ru/market-java/market-proto/tree/master/proto](https://github.yandex-team.ru/market-java/market-proto/tree/master/proto).

## Установка

```bash
npm install @yandex-market/market-proto-dts
```

## Использование

```typescript
import { SaveResultType, SaveResult } from '@yandex-market/market-proto-dts/Market/Mbo/ModelEdit';

const response: SaveResult = {
  hierarchy: {},
  type: SaveResultType.SAVE_OK,
};

if (response.type === SaveResultType.SAVE_OK) {
  // ...
}
```

## Генерация типов

Запустите команду:

```
npm install
npm run generate
```

## Сборка и публикация

Сборка пакета выполняется командой:

```
npm run build
```

Перед публикацией обновите версию в `package.json` и опубликуте в npm.yandex-team.ru:

```
npm run publish:prepare
npm publish dist
```
