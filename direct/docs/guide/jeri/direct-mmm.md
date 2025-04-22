# Mysql master monitor (direct-mmm)

## О  программе { #about }

Программа проверяет текущий мастер на основе db-config и обновляет его в нем.

### Алгоритм работы программы

1. Читает db-config из zookeeper и строит список хостов на определение мастера по шадам. Значения хостов для каждого шарда берется из 'cluster_hosts' db-config.
Список строится на основе разрешенных имен шардов, переданных через аргумент '-instances' в момент запуска программы. В deploy это задается в скипте start-mysql-master-monitor.sh(mmm->mmm-box->mysql-master-monitor->Start-command). Скрипт является частью покета, приезжающего в контейнер.
2. Для каждого нового хоста производится запуск отдельного потока(горутины), которая подключается к MySQL и проверяет его. Для определения мастера используется библитека MDB: выполняется команда 'SHOW SLAVE STATUS', который для мастера будет пустым.
3. Запущенные потоки проверок к хостам, исключенным из 'cluster_hosts', останавливаются и убираются из мониторинга.
4. Если в ходе проверки обнаруживается, что текущий мастер отличается от указанного в db-config, то производится обновление указанной записи в db-config. Запись в zookeeper возможна только при условии того, что текущий db-config свежий(не устарел ZookeeperNodeId) и не стоит стоп флаг в zookeeper(например /direct_mmm_production_stopflag). Для ТС/dev7/devtest устанавливаются аналогичные флаги в корне zookeeper дирректориию

### Пример запуска программы на dev7
Варианты запуска прописаны в скрипте start-mysql-master-monitor.sh: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-master-monitor/start-mysql-master-monitor.sh>

Ручной запуск(лги будут выводиться в stdout/stderr):
```
 /usr/local/bin/mysql-master-monitor -zkservers zkzk01a.yandex.ru:2181 -zkpath /mypath -env testing -instances ppcdata1,ppcdict,ppcmonitor
```
### Деплой контейнеры для сред
dev7: <https://deploy.yandex-team.ru/stages/direct-mmm-dev7>

devtest: <https://deploy.yandex-team.ru/stages/direct-mmm-devtest>

testing: <https://deploy.yandex-team.ru/stages/direct-mmm-testing>

prod: <https://deploy.yandex-team.ru/stages/direct-mmm-production>

### Как остановить обновление db-config
Для остановки обновления db-config, потребуется создать в zookeeper стоп флаг. Например, остановка direct-mmm в продакшене(запускать с ppcback*) выглядит так:
```
direct-zkcli touch /direct_mmm_production_stopflag
```

Для повторного восстановления работы достаточно удалить флаг:
```
direct-zkcli rm /direct_mmm_production_stopflag
```

### Мониторинг
При старте программы, запускается отдельный поток(горутина), которая отвечает за работу мониторинга. Она собирает значения о свежести db-config, свежести проверок на мастера шардов, отсутствии коллизий(нет мастеров или их несколько), отсутсвии ошибок в записи в Zookeeper и отправляет алерт в juggler.

<https://juggler.yandex-team.ru/raw_events/?query=service%3Ddirect-mysql-master-monitor-production> - production

<https://juggler.yandex-team.ru/raw_events/?query=service%3Ddirect-mysql-master-monitor-testing> - testing

<https://juggler.yandex-team.ru/raw_events/?query=service%3Ddirect-mysql-master-monitor-devtest> - devtest

<https://juggler.yandex-team.ru/raw_events/?query=service%3Ddirect-mysql-master-monitor-dev7> - dev7

### Логи
Логи работы записываются в /var/log/yandex/messages.log и отправляются в logviewer: для продакшена в <http://direct.yandex.ru/logviewer>, для остальных сред в <http://test-direct.yandex.ru/logviwer>. Например:
<https://direct.yandex.ru/logviewer/short/8ppYs41w3rwosQ> - пример поиска лога для продакшена

### API ручки(зайти в конетейнер)
<http://localhost/alive> - проверка живости программы(plain text)

<http://localhost/masters> - список текущих мастеров по шардам(hash)

<http://localhost/status> - текущее состоание проверок по шардам(hash)


### Ссылки { #links }

- Основной проект программы mysql-master-monitor: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/go-libs/cmd/mysql-master-monitor>
- Сборка пакета для deploy: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/packages/deploy/direct-mmm>
