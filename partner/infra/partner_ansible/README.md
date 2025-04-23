# partner_ansible

Пример вызова

```> ansible-playbook -v -i hosts  -l 'dev-partner2.sas.yp-c.yandex.net' install_perl_packages_with_carton.yaml```

## Соглашение про именование

В названиях плейбков/ролей используем минусы, а не подчеркивание.
(Сейчас это не так, постепенно приведем код в этом проекте к этому соглашению).

## Получить список хостов на которые нужно заказывать сертификаты

    openssl x509 -text -noout -in roles/partner2-development-cert/files/partner.yandex.ru.pem |grep DNS|perl -MData::Dumper -nalE '$c .= $_; }{ @e = sort map { s/\s*DNS://; $_ } split /,\s*/, $c; say join "\n", @e;'

Сертификаты выписываются через https://golem.yandex-team.ru/certs/
