# tap-js-api 🚀

Typescript обертки для [JS API tap-сервисов](https://yandex.ru/dev/turboapps/doc/api/about-docpage/).

> ⚠️ Исходный код пакета автоматически [публикуется на github.com](https://github.com/yandex/tap-js-api).

Пример использования:
```typescript jsx
import { getUserInfo } from '@yandex-int/tap-js-api';

getUserInfo()
    .then(user => console.log(user))
    .catch(err => console.error(err))
```


## Методы

### Приложение
- `isTurboApp(): boolean` – проверить, что приложение открыто внутри контейнера
- `setAllowHideByUserGesture(allowed: boolean): void` – управление жестом закрытия шторки контейнера
- `setPullToRefreshEnabled(enabled: boolean): void` – управление жестом pull-to-refresh
- `forceUpdateApp(): Promise<void>` – запросить форсированное обновление ресурсов турбоаппа
- `lockBottomBar(show: boolean): Promise<void>` – блокировка боттом бара в определенном состоянии
### Портальная Авторизация
- `login(): Promise<YandexPortalUserInfo>` – авторизация на портале через нативный диалог
- `logout(): Promise<void>` – разлогиниться на портале
- `getUserInfo(): Promise<YandexPortalUserInfo | null>` – информация о текущем авторизованом пользователе
- `bindPhone(params?: BindPhoneParams): Promise<void>` - привязка телефона через нативный диалог, требуется авторизация
- Типы [YandexPortalUserInfo, BindPhoneParams](src/yandex/private/portal-auth.ts)
### Авторизация для внешних пользователей
- `identifyUser(clientId: string): Promise<YandexAuthPSUIDInfo>` – проверка залогина пользвотеля
- `authorizeUser(clientId: string, scopes?: string[]): Promise<YandexAuthApiInfo>` – авторизация через нативный диалог AM
- `getCurrentUserId(clientId: string): Promise<YandexAuthPSUIDInfo | null>` – получить id пользователя
- `updateUserInfo(clientId: string): Promise<YandexAuthInfo>` – получить свежие данные пользователя
- Типы [YandexAuthPSUIDInfo, YandexAuthScope, YandexAuthApiInfo, YandexAuthInfo](src/yandex/app/auth.ts)
### Пуши
- `getPushToken(): Promise<YandexPushToken>` – получить токены для отправки пушей
- Тип [YandexPushToken](src/yandex/private/push.ts)
### Пермишены
- `requestSystemPermission(permissionName: SystemPermission, message?: string): Promise<PermissionState>` – запросить системное разрешение
- `checkSystemPermission(permissionName: SystemPermission): Promise<PermissionState>` – проверить состояние системного разрешения
- Тип [SystemPermission](src/yandex/private/system-permissions.ts)
- Тип [PermissionState](https://microsoft.github.io/PowerBI-JavaScript/modules/_node_modules_typedoc_node_modules_typescript_lib_lib_dom_d_.html#permissionstate)
### Информация о пользователе
- `getUUID(): Promise<string | null>` – получить UUID из AppMetrica
- `getDeviceId(): Promise<string | null>` – получить Device ID из AppMetrica
- `getRequestId(): string` – уникальный ID для визита в турбоапп
- `getYandexUid(): string | null` – получить значение куки yandexuid
- `getUserRegion(): Promise<YandexRegion>` – получить информацию о геопозиции пользователя
- Тип [YandexRegion](src/yandex/private/user.ts)
### Метрика
- `reportAppMetricaEvent(goal: string, attributes: object): Promise<void>` – отправить событие через AppMetrica
### Добавление сервиса на главную приложения Яндекса
- `addToNavPanel(): Promise<void>` – запросить добавление сервиса на главную приложения Яндекса


## Установка

Для установки пакета следует выполнить в корне репозитория:
```bash
npx lerna add @yandex-int/tap-js-api --scope=<package-name>
```
где `<package-name>` - название пакета, куда нужно установить `tap-js-api`.


## Ссылки

- [Интерфейсы API в браузере IDL](https://bitbucket.browser.yandex-team.ru/projects/STARDUST/repos/browser/browse/src/third_party/blink/renderer/modules/yandex/yandex.idl)
- [Интерфейсы API в браузере MOJOM](https://bitbucket.browser.yandex-team.ru/projects/STARDUST/repos/browser/browse/src/components/yandex/turboapp/api/mojom)
