# Пакет для удобной работы с апхостовым контекстом

`npm i -S @yandex-int/frontend-apphost-context`

В пакете есть интерфейс функции `main`, главный класс для работы с контекстом `ApphostContext`
и также множество типов помогающих в работе с апхостом/report-renderer, все типы можно посмотреть в `src/types.ts`.

## Как использовать

- Импортим и создаем инстанс:
```ts
import { ApphostContext, INativeApphostContext } from "@yandex-int/frontend-apphost-context";
    
const getMain = () => {
    return (_, apphostContext: INativeApphostContext) => {
        const apphostContext = new ApphostContext(apphostContext);
    };
};
```
- Далее можно либо сразу начать использовать с заранее готовыми свойствами, для самых популярных источников:
```ts
const apphostContext = new ApphostContext(apphostContext);
    
apphostContext.device // получение данных про девайс юзера
apphostContext.request // получение данных про запрос

```
- Либо отнаследоваться, добавить методов для своих источников/добавить хелперы для работы с контекстом и т. д. например:
```ts
import { ApphostContext } from "@yandex-int/frontend-apphost-context";
    
MyApphostContext extends ApphostContext {
    static MySources = {
        Ugc: 'ugc_backend'
    };
    
    get ugc() {
        return this.getSource(MyApphostContext.MySources.Ugc);
    }
}
    
const apphostContext = new MyApphostContext(apphostContext);
    
apphostContext.ugc

```
