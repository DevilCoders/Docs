# Playstation 4 Api
Пакет, призванный решить проблему работы с api playstation 4, а именно подписку и отписку от событий api.

## Прослушивание событий api playstation 4
Прослушивание событий playstation 4 api осуществляется через функцию в поле `accessfunction` в `window`: движок playstation 4 при наступлении какого-либо события или завершения команды вызывает `window.accessfunction` на top window и передает туда какие-либо данные. (подробнее см. WebMAF_Overview_e.pdf).

`@kinopoisk-int/playstation-4-api` предоставляет обертку, которая позволяет вешать много обработчиков на события api, чтобы не перезатирать значение в `window.accessfunction`.

## Использование
Пакет предоставляет функцию `patchPlaystation4API`, которая находится по пути `/src`. Функция возвращает объект, реализующий интерфейс `PlaystationAPIEventTargetInterface`:
```typescript
/**
 * Интерфейс, описывающий api, которое позволяет подписывать и отписывать несколько обработчиков на события api playstation4.
 */
interface PlaystationAPIEventTargetInterface {
    /**
     * Подписывает переданный обработчик на события api playstation 4.
     *
     * @returns функция, которая отписывает переданный обработчик от событий api.
     */
    subscribe(listener: (data: any) => void): () => void;
    /**
     * Отписывает переданный обработчик от событий api playstation 4.
     */
    unsubscribe(listener: (data: any) => void): void;
    /**
     * Отправляет команду в playstation 4 api.
     *
     * @param command название команды
     * @param params параметры команды
     */
    execute(command: string, params?: Record<string, any>): void;
}
```

Пример:
```typescript
import { patchPlaystation4API } from '@kinopoisk-int/playstation-4-api';

const playstation4Api = patchPlaystation4API(window);

const handler = (data: any) => {
    /// do something
};

const unsubscribeHandler = playstation4Api.subscribe(handler);

unsubscribeHandler();
// or
playstation4Api.unsubscribe(handler);
```
