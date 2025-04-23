## Переводы

### Хранение переводов

Переводы приложения храним в сервисе [Танкер](https://tanker.yandex-team.ru/project/travel_frontend).
Переводы из танкера выгружаются в файлы `src/i18n` с помощью пакета [i18n-sync](https://a.yandex-team.ru/arcadia/data-ui/i18n-sync).

### Доставка переводов в код

Перед сборкой кода переводы из `src/i18n`
собираются с помощью пакета [i18n-ts](https://a.yandex-team.ru/arcadia/travel/frontend/i18n-ts).

Примеры использования в коде можно посмотреть в [документации](https://a.yandex-team.ru/arcadia/travel/frontend/i18n-ts/README.md) пакета.

### React в переводах

Для встраивания React элементов, как переменных, используйте утилиту `insertJSXIntoKey`:

```tsx
insertJSXIntoKey(i18nBlock.discountFix)({
    amount: <Price currency={CurrencyType.RUB} value={amount} />,
});
```

### Workflow

При изменениях в танкере обновляем ключи в репозитории (команда обновляет файлы с переводами и собирает TS файлы)

```
npm run i18n:update
```

Если изменения из танкера подтягивать не нужно, то можно просто собрать переводы в TS файлы

```’
npm run build:i18n
```
