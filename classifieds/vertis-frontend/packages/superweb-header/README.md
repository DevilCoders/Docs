# @vertis/superapp-header

Шапка для супервеба.

Клиентская часть содержит компонент шапки.
```
import '@vertis/superweb-header/build/client.css';
import { SuperWebHeader, AppType, Mode } from '@vertis/superweb-header/build/client';
...
<SuperWebHeader
    className={ cn.superWebHeader } // опционально
    currentAppType={ AppType.CLASSIFIED } // текущий апп
    mode={ Mode.THREE_TABS } // режим - три таба или два (только автору и недвига)
/>
```

Сторибук
```
npm run storybook
```

Серверная часть содержит код для ручки синхронизации кук.

```
// www-desktop/server/index.ts
import { addSuperWebHeaderCookieSyncRoute } from '@vertis/superweb-header/build/server';
...
addSuperWebHeaderCookieSyncRoute(app);

```

