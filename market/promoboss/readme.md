## Начало работы с проектом
Для генерации проекта для Intellij IDEA выполните:

```
cd ~/arcadia/market/promoboss/
sh generate_project.sh -i ~/arc_projects/ -a ~/arcadia/
```

По умолчанию проект создается в директории ~/arc_projects/promoboss.

## Локальный запуск
Для локального запуска нужно в Idea использовать сгенерированную конфигурацию ```Run Service (generated)```.

Используется embedded база данных.

Сервис запускается на порту 8081 для возможности паралелльного локального запуска с другими сервисами.
Порт можно изменить в файле
```src/main/properties.d/local/00_application.properties```, свойство ```server.port```.

