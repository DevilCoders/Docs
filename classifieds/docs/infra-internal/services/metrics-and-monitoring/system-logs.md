## Как реализовано

1. Поставка системных логов реализована с помощью утилиты [vector](https://vector.dev)  
2. Конфигурируется одноименной [ролью](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-ansible/roles/vector) в vertis-ansible.  
3. Логи отправляются в logs-collector
4. Доступны в  http://grafana.vertis.yandex-team.ru (документация [тут](https://docs.yandex-team.ru/classifieds-infra/logs/grafana)).  

##  Как смотреть/делать запросы

1. Выбираем ``service=journalctl``
2. Указываем нужный фильтр по которому нужно найти записи, примеры описаны ниже.

Для поиска всех событий на хосте ``docker-01-sas.prod.vertis.yandex.net``:  
``service=journalctl host=docker-01-sas.prod.vertis.yandex.net``  
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-05-26%20%D0%B2%2015.28.38.png">

Для поиска всех событий nomad клиентов на докер серверах в сасово:  
``service=journalctl host=docker-*-sas.prod.vertis.yandex.net _SYSTEMD_UNIT=nomad.service``  
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-05-26%20%D0%B2%2015.28.15.png">

Для поиска всех событий на сервере ``docker-cloud-19-sas.test.vertis.yandex.net`` которые содержат запись про ``unregister_netdevice``  
``service=journalctl host=docker-cloud-19-sas.test.vertis.yandex.net message=*unregister_netdevice*``  
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-05-26%20%D0%B2%2015.36.14.png" >  

[Ссылка на snapshot c примером](https://grafana.vertis.yandex-team.ru/s/t/PBw6xNRs57LkBd)
