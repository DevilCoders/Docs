# @yandex/tap-js-api 🚀

Typescript обертки для [JS API tap-сервисов](https://yandex.ru/dev/turboapps/doc/api/about-docpage/).

Пример использования:
```typescript jsx
import { identifyUser } from '@yandex/tap-js-api';

identifyUser()
    .then(user => console.log(user))
    .catch(err => console.error(err))
```


## Методы

- **Приложение**
    - `isTurboApp(): boolean` – проверить, что приложение открыто внутри контейнера
    - `setAllowHideByUserGesture(allowed: boolean): void` – управление жестом закрытия шторки контейнера
    - `setPullToRefreshEnabled(enabled: boolean): void` – управление жестом pull-to-refresh
    - `forceUpdateApp(): Promise<void>` – запросить форсированное обновление ресурсов турбоаппа
    - `lockBottomBar(show: boolean): Promise<void>` – блокировка боттом бара в определенном состоянии
- **Авторизация**
    - `identifyUser(clientId: string): Promise<YandexAuthPSUIDInfo>` – проверка залогина пользвотеля
    - `authorizeUser(clientId: string, scopes?: string[]): Promise<YandexAuthApiInfo>` – авторизация через нативный диалог AM
    - `getCurrentUserId(clientId: string): Promise<YandexAuthPSUIDInfo | null>` – получить id пользователя
    - `updateUserInfo(clientId: string): Promise<YandexAuthInfo>` – получить свежие данные пользователя
    - Типы [YandexAuthPSUIDInfo, YandexAuthScope, YandexAuthApiInfo, YandexAuthInfo](src/yandex/app/auth.ts)
- **Метрика**
    - `reportAppMetricaEvent(goal: string, attributes: object): Promise<void>` – отправить событие через AppMetrica


## Установка

```bash
npm install --save git+ssh://github.com/yandex/tap-js-api#v0.4.0
```
