# arcadia_node

Самописные скрипты для компиляции фронта с использованием node, yarn и так далее.  
Так как на (октября 2019) в аркадии не было сборки фронта.

## Как обновить версию node

Команда загружает node.js и создает файл `nodes/node@<VERSION>.ya.make`

```bash
./scripts/node_download.sh --version 10.7.0
```

## Как обновить node_modules

Команда создает папку node_modules, выгружает ее в сендбокс и меняет файл node_modules.ya.make

```bash
cd path_to_folder_with_package-lock.json
./scripts/node_modules_update.sh --output-file node_modules.ya.make
```

