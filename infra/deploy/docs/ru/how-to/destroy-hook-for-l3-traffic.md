# Destroy policy для проверки отсутствия трафика

## Описание

При изменении вычислительных ресурсов подов происходит перенос подов на другие хосты со сменой IP-адреса. Возможна ситуация, когда список адресов, известных клиентам (балансеры, apphost) отличается от списка актуальных адресов сервиса, так как Деплой перевозит инстансы без учета фидбека от клиентов. Для обеспечения безопасных переездов подов есть возможность установить destroy-hook.

## Как установить

### Шаг 1. Добавить новый box

```
Name: destroy_hook
Base layer: xenial-app
Additional layers:
   ID: ulogd
   URL: rbtorrent:98e071f4f7b9054c02552169034b7f05bd1cee14
Static resources:
   ID: destroy_hook
   URL: rbtorrent:b168c2021181b3fd7cd395bd226b7976499407e5
   Mount point: /destroy_hook
```
![add_new_box](https://jing.yandex-team.ru/files/i-dyachkov/destroy_hook_for_l3_1.png)


### Шаг 2. В box добавить workload

```
Name: wait-port-80-connections
Start command:  /bin/sleep infinity
Readiness probe: 
    Exec: test ! -f /tmp/destroy.flag
Destroy policy:
    Exec: ./destroy_hook/check_destroy.sh
    Max tries: 1
Environment variables:
   PORT: 80 
```
![add_new_workload](https://jing.yandex-team.ru/files/i-dyachkov/destroy_hook_for_l3_2.png)

## Примечания

- destroy-hook должен смотреть на тот порт, по которому L3-балансер делает health-check

- destroy-hook не отработает в случае, когда полностью удаляется кластер из конфига. Для того, чтобы избежать проливания траффика, необходимо сначала уменьшить количество подов до 0, и только когда они будут удалены контроллером, можно удалять кластер из конфигурации.

- в случаях, когда приложение принимает трафик на нескольких портах, есть возможность добавить workload в destroy-hook, порт конфигурируется при помощи environment: PORT

## Детали реализации

[Детали реализации команды destroy policy для проверки отсутствия трафика](https://wiki.yandex-team.ru/users/frolstas/pod-safe-removal-draft/#detalirealizaciikomandydestroypolicydljaproverkiotsutstvijatrafika)
