# Inforctl
Скрипт для управления сервисами WMS

# Requirenments
Для сборки Inforctl требуются следующие компоненты:

* golang 1.16.3+

### How to build
Для сборки утилиты для работы из под linux можно воспользовать следующей командой
```shell
env GOOS=linux GOARCH=amd64 go build 
```

### Usage
```shell
inforctl start

scprd-api  active (running)
scprd-wmoltp@1  active (running)
scprd-wmbatch@1  active (running)
scprd-excelplugin@1  active (running)
scprd-uiservice@1  active (running)
scprd-wmsocket@1  active (running)
scprd-reports@1  active (running)
```

### Arguments
* start - запускает все сервисы
* stop - отсанавалиается все сервисы
* restart - перезапускает все сервисы
* enable - сервисы будут запускать при запуске системы
* status - статус сервисов

### Архив
На архивной ноде все сервисы запускать не нужно, для такого случая есть аргумент
'-s'. В этом случае inforctl запустить только те сервисы, который должны работать на архиве.

Пример:
```bash
inforctl start -s
```

### Конфигурационный файл

Для работы скрипта требуется создать конфигурационный файл (если его еще нет)
/etc/yandex/inforconf.yaml со следующим содержанием:

```yaml
logPath: /var/log/infor/inforctl/inforctl.log
envPath: /etc/yandex/environment.type
services:
  - name: scprd-api.service
    runOnArchive: true
    doNotStartOnProd: true
  - name: scprd-wmoltp@$NODE.service
    runOnArchive: true
```

* logPath - путь до файла где inforctl будет сохранять логи
* envPath - путь до файла указанием типа среды (testing, prestable, production)
* services - список systemd units которым управляет inforctl
  
Параметры сервисов:
* name - название systemd unit, название может содержать параметр $NODE вместо которого будет подставлен номер ноды
* runOnArchive - флаг для запуска сервиса на архивной ноде
* doNotStartOnProd - флаг для игнорирования сервиса в production окружении
