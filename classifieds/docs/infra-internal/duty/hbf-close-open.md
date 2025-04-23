# Закрытие (открытие) с помощью HBF

## Управление HBF через firewall.yandex-team.ru

Красиво и удобно закрыться можно через https://firewall.yandex-team.ru/drills по кнопке `Add drill`.

Для учений в MYT обязательно в исключения добавляем hadoop: `_C_VERTIS_PROD_HDP_L3TOR_`.

Для закрытия указываем следующие проекты в поле `Projects`:
* `_VERTISPRODNETS_`
* `_VERTISPRODCLOUDNETS_`
* `_CLOUD_YANDEX_CLIENTS_VERTISPROD_NETS_`

## Закрываем/открываем отдельные сервера с помощью hbf-mngr.sh

На каждом сервере расположен скрипт [hbf-mngr.sh](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-hbf-agent-config/src/usr/sbin/hbf-mngr.sh). Он позволяет:
* Закрыть хост от нагрузки: `hbf-mngr.sh close`
* Открыть хост для нагрузки: `hbf-mngr.sh open`
* Проверить наличие нужных конфигов и показать какой сейчас актуален: `hbf-mngr.sh check`
* Перезапустить hbf-agent: `hbf-mngr.sh restart`

## Закрываем/открываем кластера с помощью hbf-mngr.sh

Используем плейбуки из репозитория vertis-ansible:
* [hbf_close.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/vertis-ansible/hbf_close.yml) - закрывает группу хостов.
* [hbf_open.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/vertis-ansible/hbf_open.yml) - открывает группу хостов.

Пример запуска:
```
ansible-playbook hbf_open.yml -e "host=vertis_test_shard dc=myt"
ansible-playbook hbf_close.yml -e "host=vertis_vprod_docker dc=myt"
```
