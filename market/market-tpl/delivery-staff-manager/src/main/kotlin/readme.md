# Delivery staff manager

## Локальный запуск

Запустить скрипт
```shell
./generate_project.sh
```
Появится проект идеи по пути ```~/idea_projects/delivery-staff-manager```. В проекте запустить конфигурацию ```Run Service```

### Запуск зависимостей

```shell
docker-compose -f dependency-stubs/docker-compose.yml up -d
```

### Swagger

http://localhost:8081/swagger-ui/index.html
