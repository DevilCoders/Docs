# production mysql base image

Образ, может (должен) быть использован как базовый для выполнения различных работ с продуктовыми бэкапами mysql. По существу берет бэкап из s3, расшифровывает ключами из секретницы и разворачивает внутри контейнера, комманда `/opt/bin/mysql-init-slave.sh any` должна быть частью **вашего** обработчика/скрипта

- Скрипту передается название инстанса для развертывания из backup (<https://wiki.yandex-team.ru/vertis-admin/storage/mysql/>)
- В stream режиме backup доставляется внутрь контейнера `curl .. | ssl .. | tar .. -C /path`
- В **фоне** запускается mysql
- Ресурсы mysql - минимальны, **не предназначено** для тестирования/разработки, запускается **без авторизации и сети** с доступом по сокету внутри контейнера

## Usage

```Docker
FROM FROM registry.yandex.net/vertis/mysql-base:latest

CMD /opt/bin/mysql-init-slave.sh logs
    or
CMD /opt/bin/mysql-init-slave.sh archive
    or
CMD /opt/bin/mysql-init-slave.sh any
```
