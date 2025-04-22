# @yandex-int/fix-version

Модуль устанавливает FixVersion для Трекера.
Можно использовать, чтобы связавать версии в npm с задачами в трекере.

## Использование

### Внутри пакета монорепозитория

Добавьте в какой-то из скриптов, которые запускаются из мастера запуск программы (например, `ci:deploy:master`):

```
DEBUG=* npx @yandex-int/fix-version
```

### CLI
```bash
npx @yandex-int/fix-version --help
```

### node api
Модулем можно пользоваться в других node js программах.
Для этого достаточно импортировать модуль.

```js
import { StVersionClient } from '@yandex-int/fix-version/build/st/api'

// сконфигурировать клиент
const client = new StVersionClient('token', 'queque');

// и пользоваться
client.setSTVersion(params);

```

## Разработка

```bash
npm ci
npm start
```
