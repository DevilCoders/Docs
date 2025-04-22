# Delivery Staff Manager

Основан на фреймворке [MJ](https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/)
<br/>
[Yandex.Deploy](https://yd.yandex-team.ru/projects/market-delivery-staff-manager)
<br/>
[TSUM](https://tsum.yandex-team.ru/pipe/projects/market-3pl/delivery-dashboard/delivery-staff-manager)

### Генерация

Предварительно создать папку ```~/idea_projects/delivery-staff-manager```.
Из корня проекта запустить:
```shell
./generate_project.sh
```
В указанной папке будет сгенерирован проект для idea

### Запуск

При генерации проекта создается конфигурация idea для запуска по умолчанию ```Run service (generated)```.
Так же для запуска понадобиться локальная БД, поднять которую можно командой:
```shell
docker-compose -f dependency-stubs/docker-compose.yml up -d
```

### Open API

Open API спецификацию можно найти здесь:
```
src/main/resources/openapi/api/api.yaml
```
При внесении изменений необходимо запускать ```ya ide``` для генерации по спецификации
