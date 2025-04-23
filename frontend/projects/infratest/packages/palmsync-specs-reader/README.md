# palmsync-specs-reader

Модуль позволяет читать `*testpalm.yml` файлы, опираясь на конфиг `.palmsync.conf.js`

## Установка
```sh
npm install @yandex-int/palmsync-specs-reader --registry http://npm.yandex-team.ru
```

## API

### `read`(projectPath: **string**): **Promise**
Аргументы:
 - `projectPath`: путь к проекту. По умолчанию - `process.cwd()`;

Структура возвращаемого объекта:
```ts
result.<testpalm_file_name> = <parsed_yaml_content>
```

Пример использования:
```ts
import {read} from "@yandex-int/palmsync-specs-reader"

const files = await read("path_to_another_project");
```
