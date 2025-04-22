# **Deplate**
## **Stage**
### **Update**
Обновление стейджа:
```shell
cmd/deplate/deplate [--arc-path path] [--dry-run] [--token-path path] stage update STAGE_NAME STAGE_VALUES [-l LAYER_NAME:12345678]
```
* `--arc-path` Путь к аркадии, вычисляется автоматически если вызвать из аркадии
* `--dry-run` Запуск без применения изменений
* `--token-path` Путь до токена, по умолчанию `~/.deplate/token`, получается по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=30d03820961e4b038e3575af4077e258), так же можно передать черех `DEPLATE_TOKEN` или `DEPLATE_TOKEN_PATH`
* `STAGE_NAME` Имя deploy стейджа
* `STAGE_VALUES` Путь до файла с перемеными для стейджа
* `-l` Задает версию слоя (по умолчанию они берутся из запущеного стейджа)

Пример:
```shell
cmd/deplate/deplate stage update --debug testing_isonami-service marketito/testing/testing_isonami-service.yaml
```

## **Values**
### **Get**
Получение параметров с которомы сгенерирован активная ревизия стейджа:
```shell
cmd/deplate/deplate [--arc-path path] [--dry-run] [--token-path path] values get STAGE_NAME
```
* `--arc-path` Путь к аркадии, вычисляется автоматически если вызвать из аркадии
* `--dry-run` Запуск без применения изменений
* `--token-path` Путь до токена, по умолчанию `~/.deplate/token`, получается по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=30d03820961e4b038e3575af4077e258), так же можно передать черех `DEPLATE_TOKEN` или `DEPLATE_TOKEN_PATH`
* `STAGE_NAME` Имя deploy стейджа

Пример:
```shell
cmd/deplate/deplate values get testing_isonami-service
```
