# Github-Runners

## Общая информация
Гитхаб-раннеры - виртуальные машины, на которых выполняются github actions. Текущая конфигурация раннеров предусматривает, что мы везем минимальное число пакетов для запускаемых на них экшенах, а экшены в свою очередь - запускаются в докере или используют шаги, в которых инфраструктура экшена конфигурируется и удаляется после выполнения экшена самостоятельно.

У нас есть [дашборд](https://grafana.vertis.yandex-team.ru/d/TAGLdveMk/gh-runners?orgId=1&from=now-24h&to=now) в графане, который отражает всю статистику по гитхаб раннерам и экшенам: количество свободных и занятых раннеров, количество запущенных экшен-джоб и количество экшен-джоб в очереди.
Метрики в графану перекладываются сервисом [github-metrics](https://a.yandex-team.ru/arc_vcs/classifieds/infra/github-metrics), который живет в шиве.

Кондукторная группа: `vertis_vdev_gh_cloud`

FQDN: `gh-cloud-<index>-<dc>.dev.vertis.yandex.net`

Пул адресов: `2a02:6b8:c02:900:1:d:0:bb<index>`

## Управление кластером

Раннеры живут в Яндекс Облаке в инстанс-группах.
Конфигурируются через terraform с помощью [конфига](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse/compute/vertis_vdev_gh_cloud/vertis_vdev_gh_cloud.tf).

## Как правильно и красиво запустить или выключить раннер

На всех гитхаб-раннерах лежит скрипт `gh-mngr.sh`, с помощью которого рекомендуется управлять процессами агента из-под рута.
По ключу `--help` можно ознакомиться с подробной инструкцией по использованию скрипта.
* `--enable` может поднять раннер-процессс с нуля, выполняется полный цикл запуска;
* `--run` просто запускает раннер-процесс. Можно использовать после того, как раннер-процесс был остановлен;
* `--stop` останавливает раннер-процесс;
* `--disable` останавливает раннер-процесс и отключает раннер на гитхабе.

## Как правильно запустить и выключить раннер в ручном режиме
### Запуск
* Получить регистрационный токен
```
sudo su
KEY=$(yav get version --rsa-private-key /root/.ssh/id_rsa_datasources --rsa-login robot-vertis-yav-tst ver-01f9c5kf673zw5rgjx6s04vxs2 --json | jq ".value.OK_private_key_64" | sed 's/\"//g'); /usr/bin/runner_token -token registration -key ${KEY}
```
* Зарегистрировать хост на гитхабе
```
su robot-vertis-repo
cd /var/lib/gh-runner/ && bash config.sh --url https://github.com/YandexClassifieds --name $(hostname -f) --token $(cat /etc/registration_token) --labels $(hostname -f),ops,XL && echo "true"; touch /var/lib/gh-runner/configured
```
* Установить сервис Runner
```
su robot-vertis-repo
cd /var/lib/gh-runner/ && sudo ./svc.sh install
```
* Запустить сервис Runner
```
su robot-vertis-repo
cd /var/lib/gh-runner/ && sudo ./svc.sh start
```

## Выключение
* Остановить сервис Runner
```
su robot-vertis-repo
cd /var/lib/gh-runner && sudo ./svc.sh stop
```
* Удалить сервис Runner
```
su robot-vertis-repo
cd /var/lib/gh-runner && sudo ./svc.sh uninstall
```
* Получить токен разрегистрации
```
sudo su
KEY=$(sudo yav get version --rsa-private-key /root/.ssh/id_rsa_datasources --rsa-login robot-vertis-yav-tst ver-01f9c5kf673zw5rgjx6s04vxs2 --json | jq ".value.OK_private_key_64" | sed 's/\"//g')
/usr/bin/runner_token -token remove -key ${KEY}
```
* Разрегистрировать раннер
```
su robot-vertis-repo
cd /var/lib/gh-runner && ./config.sh remove --token $(cat /etc/remove_token)
```
