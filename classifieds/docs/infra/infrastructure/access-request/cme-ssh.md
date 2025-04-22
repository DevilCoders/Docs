# Работа с кластерами CM.Expert после переезда

## Общая информация

Переезд кластеров CME осуществляется на dualstack-сети и вертикальный образ диска с интеграцией инфраструктуры.

Это необходимо по следующим причинам:
* Переиспользование инфраструктуры Вертикалей и Яндекса на серверах;
* Использование системы [CAuth](https://wiki.yandex-team.ru/intranet/idm/cauthmanual/) вместо ldap для авторизации пользователей по ssh;
* Ключевая причина - для обеспечения сетевого доступа из сервисов CME в сервисы Вертикалей и в обратную сторону; для возможности использования внутренних сервисов Яндекса (например, [секретница](https://yav.yandex-team.ru/)) в сервисах CME.

## Кластера, переехавшие в dualstack {#clusters}

У каждого хоста есть **два хостнейма**, которые работают для **разных** VPN. Хостнейм для VPN CME не будет доступен из-под VPN Yandex, а хостнейм для VPN Yandex не будет доступен из-под VPN CME.

### Gitlab

* Билдеры - `vertis_vdev_cme_gitlab_builder`
    * `gitlab-builder-01-sas.dev.vertis.yandex.net`
    * `gitlab-builder-01-vla.dev.vertis.yandex.net`
    * `gitlab-builder-01-myt.dev.vertis.yandex.net`
* Сервер - `vertis_vprod_cme_gitlab_srv`
    * `gitlab-srv-01-sas.prod.vertis.yandex.net`

### preproduction

* docker - `vertis_vtest_cme_docker`
    * `cme-docker-01-sas-test.ru-central1.internal` (ipv4, VPN CME) /`cme-docker-01-sas.test.vertis.yandex.net` (ipv6, VPN Yandex)
    * `cme-docker-01-myt-test.ru-central1.internal` (ipv4, VPN CME) /`cme-docker-01-myt.test.vertis.yandex.net` (ipv6, VPN Yandex)
* web - `vertis_vtest_cme_web`
    * `cme-web-01-sas-test.ru-central1.internal` (ipv4, VPN CME) /`cme-web-01-sas.test.vertis.yandex.net` (ipv6, VPN Yandex)
    * `cme-web-01-myt-test.ru-central1.internal` (ipv4, VPN CME) /`cme-web-01-myt.test.vertis.yandex.net` (ipv6, VPN Yandex)
* estimator - `vertis_vtest_cme_estimator`
    * `cme-estimator-01-vla-test.ru-central1.internal`
    * `cme-estimator-01-sas-test.ru-central1.internal`
* multipython - `vertis_vtest_cme_multipython`
    * `cme-multipython-01-sas-test.ru-central1.internal`
    * `cme-multipython-01-vla-test.ru-central1.internal`
    * `cme-multipython-01-myt-test.ru-central1.internal`
* lb-internal - `vertis_vtest_cme_lb_int`
    * `cme-lb-int-01-sas.test.vertis.yandex.net`
    * `cme-lb-int-01-vla.test.vertis.yandex.net`
* lb-external - `vertis_vtest_cme_lb_ext`
    * `cme-lb-ext-01-sas.test.vertis.yandex.net`
    * `cme-lb-ext-01-vla.test.vertis.yandex.net`

### production
* docker - `vertis_vprod_cme_docker`
    * `cme-docker-01-sas-prod.ru-central1.internal` (ipv4, VPN CME) / `cme-docker-01-sas.prod.vertis.yandex.net` (ipv6, VPN Yandex)
    * `cme-docker-02-sas-prod.ru-central1.internal` (ipv4, VPN CME) / `cme-docker-02-sas.prod.vertis.yandex.net` (ipv6, VPN Yandex)
    * `cme-docker-01-vla-prod.ru-central1.internal` (ipv4, VPN CME) / `cme-docker-01-vla.prod.vertis.yandex.net` (ipv6, VPN Yandex)
    * `cme-docker-01-myt-prod.ru-central1.internal` (ipv4, VPN CME) / `cme-docker-01-myt.prod.vertis.yandex.net` (ipv6, VPN Yandex)
* web - `vertis_vprod_cme_web`
    * `cme-web-01-sas-prod.ru-central1.internal`
    * `cme-web-02-sas-prod.ru-central1.internal`
    * `cme-web-03-sas-prod.ru-central1.internal`
    * `cme-web-04-sas-prod.ru-central1.internal`
    * `cme-web-01-vla-prod.ru-central1.internal`
    * `cme-web-02-vla-prod.ru-central1.internal`
    * `cme-web-03-vla-prod.ru-central1.internal`
    * `cme-web-04-vla-prod.ru-central1.internal`
    * `cme-web-01-myt-prod.ru-central1.internal`
    * `cme-web-02-myt-prod.ru-central1.internal`
    * `cme-web-03-myt-prod.ru-central1.internal`
    * `cme-web-04-myt-prod.ru-central1.internal`
* lb-internal - `vertis_vprod_cme_lb_int`
    * `cme-lb-int-01-sas.prod.vertis.yandex.net`
    * `cme-lb-int-01-vla.prod.vertis.yandex.net`
* lb-external - `vertis_vprod_cme_lb_ext`
    * `cme-lb-ext-01-sas.prod.vertis.yandex.net`
    * `cme-lb-ext-01-vla.prod.vertis.yandex.net`
* estimator - `vertis_vprod_cme_estimator`
    * `cme-estimator-01-vla-prod.ru-central1.internal`
    * `cme-estimator-01-sas-prod.ru-central1.internal`
    * `cme-estimator-02-sas-prod.ru-central1.internal`
    * `cme-estimator-01-myt-prod.ru-central1.internal`
* multipython - `vertis_vprod_cme_multipython`
    * `cme-multipython-01-sas-prod.ru-central1.internal`
    * `cme-multipython-01-vla-prod.ru-central1.internal`
    * `cme-multipython-01-myt-prod.ru-central1.internal`

## Доступы на хосты по ssh

Иногда для дебага или просмотра логов требуется доступ по ssh на хосты.

Для того, чтобы ssh в общем случае работал, нужно выполнить обязательные условия - **добавить на staff свой публичный ssh-ключ** и при попытке коннекта к хосту использовать **логин со стаффа**.

### Как заказать ssh и sudo

Для заказа ssh и sudo используется система [IDM](https://idm.yandex-team.ru).

1. Зайти на [IDM](https://idm.yandex-team.ru) и нажать кнопку "Запросить роль".

    ![get_role.png](images/get_role.png)

2. В качестве системы в верхнем поле необходимо выбрать `CAuth`, назначение - `conductor.<название группы хостов>`. Группы хостов можно узнать в разделе [Кластера, переехавшие в dualstack](cme-ssh.md#clusters) этой доки. В качестве примера укажем `conductor.vertis_vtest_cme_docker`. Далее - выбрать необходимую роль:
    * `ssh` - доступ уже выдан для хостов preproduction, поэтому для них заказывать дополнительно не нужно;
    * `sudo` - для production дополнительно потребуется заказать роль `ssh`.

    ![requested_role.png](images/requested_role.png)

3. Если вы заказываете роль `sudo` - в окошке `role` необходимо выбрать `ALL=(ALL) NOPASSWD: ALL`.

    ![sudo_rules.png](images/sudo_rules.png)

4. Необходимо выбрать срок действия роли. Мы выдаем только **временные** роли по требованиям СИБ. Поэтому оцените срок, на который вам требуются эти роли, и укажите его. Если вам нужен доступ на постоянной основе - вам придется регулярно его перезапрашивать. Бессрочные заявки и заявки на 10 лет мы **отклоняем**.

    ![role_valid_time.png](images/role_valid_time.png)

5. Обоснуйте необходимость заказа роли в соответствующем поле и по возможности приложите тикет, в рамках которого нужен доступ.

    {% cut "Пример того, как будет выглядеть ваша роль" %}

    ![whole_role.png](images/whole_role.png)

    {% endcut %}

6. Нажмите кнопку "Запросить" в самом конце страницы.

### Апрувы ролей

Роли подтверждает [Группа эксплуатации Вертикальных сервисов](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra_mnt/).

После апрува ваш доступ прорастет в течение **15-30 минут** после апрува заявки.

Новые заявки регулярно просматриваются, но если вам необходим **экстренный** апрув заявки - можно обратиться со ссылкой на заявку в чат `verticals-duty`, к дежурному админу или к одному из апруверов в будний день. В выходной день - обращаться к дежурному админу или через чат `verticals-duty` с призывом дежурного админа.

По всем вопросам о получении ssh-доступов можно обратиться в чат `verticals-duty`.
