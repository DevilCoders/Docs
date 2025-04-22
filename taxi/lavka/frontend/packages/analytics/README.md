# Analytics

## Структура

- `src/lib/metrika-contract.ts` - proxy-обертка над реализацией метрики
- `src/analytics` - описание событий аналитики

## Использование

### 1. Реализация провайдера на уровне проекта

```ts
import {BaseMetrikaProvider} from '@lavka/analytics'

// нужно реализовать отправку событий яндекс.метрики
class AppMetrika extends BaseMetrikaProvider {
  reachGoal<T extends keyof IMetrikaEvents>(
    event: T,
    logHandler: IMetrikaLogHandler<T> | IMetrikaEvents[T],
    clearData = true,
  ) {
    /* ... */
  }

  hit(url: string, options?: IMetrikaHitOptions) {
    /* ... */
  }
}

// выставить провайдера
setProvider(new AppMetrika())
```

### 2. Отправка событий

```ts
import {addressSearchAnalytics} from '@lavka/analytics'

addressSearchAnalytics.opened({
  /*...*/
})
```
