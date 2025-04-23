# Полезности
## Настройка IntelliJ плагина [Protocol Buffers](https://plugins.jetbrains.com/plugin/14004-protocol-buffers/)

1. Идем в конфиг плагина: Preferences -> Languages & Frameworks -> Protocol Buffers
2. Выключаем "Configure automatically"
3. Добавляем путь к папке proto: <путь до проекта>/schema-registry/proto
4. Если у вас проблема с импортом google/protobuf:
   явно добавить путь до места где хранятся его proto по аналогии п.3
   у меня этот путь такой /usr/local/Cellar/protobuf/3.17.3/include.

кроме того в настройках плагина у вас может гореть красным "Descriptor Path" - п.4 должен решить эту проблему
