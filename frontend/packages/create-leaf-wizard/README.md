#create-leaf-wizard
## Usage 
  <!-- usage -->
```sh-session
$ npm install -g @yandex-int/create-leaf-wizard
$ create-leaf-wizard COMMAND
running command...
$ create-leaf-wizard (-v|--version|version)
@yandex-int/create-leaf-wizard/1.7.7 linux-x64 node-v12.18.1
$ create-leaf-wizard --help [COMMAND]
USAGE
  $ create-leaf-wizard COMMAND
...
```
<!-- usagestop -->

##Пример конфига:
```json
{
  "service": {
    "leafType": "package", // Тип листа (package | service)
    "path": "./services/stub/", //путь до стаба относительно корня монорепозитория
    "description"?: "stub description", // Описание стаба
    "blackListPaths": [ //список файлов и директорий, которые не нужно копировать в новый лист
      '/__reports',
      '/node_modules',
      '/package-lock.json',
      '/build'
    ],
    "npmScript"?: "prepare-stub" // скрипт из package.json стаба, который выполнится после установки зависимостей листа
  }
}
```
