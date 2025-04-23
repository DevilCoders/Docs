# callcenter-staff

Общие компоненты, утилиты, типы и прочее для приложений Коллцентра

## Установка

Для установки пакета следует выполнить в корне репозитория:
```bash
npx lerna add @yandex-taxi/callcenter-staff --scope=<package-name>
```
где `<package-name>` - название пакета, куда надо поставить `callcenter-staff`.

Пример использования:
```jsx
import {server} from '@yandex-taxi/callcenter-staff/bunker';

console.log(server.version);
```
