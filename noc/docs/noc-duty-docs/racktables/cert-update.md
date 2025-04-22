# Обновление сертификата
## Назначение
Данное руководство разработано с целью разъяснения основных шагов по обновлению и замене сертификата основного и резервных web-серверов [Racktables](https://racktables.yandex-team.ru/).

[Перейти сразу к инструкции](cert-update/#manual)  
[Перейти сразу к замене на серверах](cert-update/#commands)

## Целевая аудитория
* Новые сотрудники NOCDEV
* Дежурные инженеры NOCDEV
* Сотрудники ответственные за эксплуатацию сервисов Racktables

## Основания для разработки руководства
* На момент написания руководства срок жизни сертификата RT составляет всего полгода.
* В зависимости от срока жизни и типа сертификата срабатывает [проверка Mondata](https://noc-gitlab.yandex-team.ru/nocdev/mondata/-/blob/master/check/certcheck.sh)
* Процедура обновления сопряжена с согласованиями в СИБ (~~и глупыми вопросами~~)
* Разные процедуры для noc-\*, man1-rt1 и салтовых нодах (не ошибиться с копипастой)

## Область применения 
Продовые сервера RT. У staging и prestable другие сертификаты.

## Процедура обновления {#manual}
### Заказать сертификат
1. Перейти в [Сертификатор](https://crt.yandex-team.ru/certificates/3307307?serial_number=&common_name=racktables.yandex.net) и найти "racktables.yandex.net"
2. Перезапросить 
3. Заполнить поля по аналогии со старыми сертификатами
4. Дождаться создания заявки SECTASK-*
5. Если робот спрашивает про AWACS - ответить, что ***"Racktables не использует deploy или awacs, а сервера железные."***
6. После согласования robot-crt@ пришлёт на почту ссылку на сертификат в [секретнице](https://yav.yandex-team.ru)
7. Добавить доступ на чтение к секрету для "Салтовод Конфигович (robot-nocdev-salt)"
8. Забрать сертификат (***racktables.yandex-team.ru.pem***) и ключ (***racktables.yandex-team.ru.key***).
 Сертификатор отдаёт только .pem, ключ надо копировать отдельно из секретницы.

### Внести изменения в салт
Поправить ссылки на секретницу в /trunk/arcadia/admins/salt-media/noc/pillar/nocdev-rt.sls .
Сделать PR, получить одобрение, вмержить.

### Завести NOCRFCS
* [форма](https://forms.yandex-team.ru/surveys/21525/)
* [пример](https://st.yandex-team.ru/NOCRFCS-7887)

### Заменить сертификаты {#commands}
Сначала меняем и проверяем на резервных серверах (`ls -l /home/racktables/master`).  
На мастере в последнюю очередь.

**Обновление на салтовых нодах:**
Проверить, что салт собирается сделать всё правильно
```
sudo salt-call state.highstate test=True
```
И выкатить
```
sudo salt-call state.highstate
```
nignx reload салт сделает сам.

**Расположение сертификатов и nginx на Freebsd (noc-\*:**
```
# symlink /usr/local/etc/nginx/certs -> /usr/local/configs/nginx/certs
/usr/local/configs/nginx/certs/racktables.yandex-team.ru.key
/usr/local/configs/nginx/certs/racktables.yandex-team.ru.pem
/usr/local/etc/rc.d/nginx
```

**Расположение сертификатов и nginx на Ubuntu (man1-rt1):**
```
/etc/nginx/certs/racktables.yandex-team.ru.key
/etc/nginx/certs/racktables.yandex-team.ru.pem
/etc/init.d/nginx
```
Внимание: директории /usr/local/configs/ являются git-репозиторием. ./certs/ должны игнорироваться.

1) Скопировать и переименовать действующие сертификаты на случай отката
***racktables.yandex-team.ru.key.old***
***racktables.yandex-team.ru.pem.old***
2) Заменить действующие сертификат и ключ на свежие
3) Перезапустить(именно **reload**) nginx

    **FreeBSD**
    ```
    $ sudo /usr/local/etc/rc.d/nginx reload
    Performing sanity check on nginx configuration:
    nginx: the configuration file /usr/local/etc/nginx/nginx.conf syntax is ok
    nginx: configuration file /usr/local/etc/nginx/nginx.conf test is successful
    ```
    **Ubuntu**
    ```
    $ sudo /etc/init.d/nginx reload
    [ ok ] Reloading nginx configuration (via systemctl): nginx.service.
    ```
4) Проверяем дату и сертификат
    ```
    openssl s_client -showcerts -connect localhost:443 < /dev/null | openssl x509 -text
    ```
5) Проверяем fingerprint 
    ```
    openssl x509 -in /usr/local/etc/nginx/certs/racktables.yandex-team.ru.pem -noout -fingerprint -sha256
    ```
6) После смены на мастере проверяем в браузере
