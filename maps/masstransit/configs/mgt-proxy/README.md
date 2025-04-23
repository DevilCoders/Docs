Этот код используется для доставки расписаний мосгортранса в карты. Подробнее про это можно почитать на вики: https://wiki.yandex-team.ru/users/bugsbunny/MGT/

# Конфиги для прокси к расписаниям МГТ

Тут находится скрипт, с помощью которого можно поднять прокси во внутреннюю сеть мосгортранса, чтобы скачивать оттуда расписания общественного транспорта.

Скрипт кладет на машину:
- Конфиг для клиента OpenVPN.
- Правила iptables, закрывающие машину от сети МГТ.
- Конфиг nginx, который используется в качестве прокси к сайту МГТ.


## Как использовать

- Берем машину с Ubuntu Xenial.
- Запускаем на ней скрипт `./setup_proxy.sh`.
- Потом добавляем в папку `/etc/openvpn` файлы `ca.crt`, `ta.key`, `yandex.crt` и `yandex.key`, которые я не положил сюда, потому что они возможно секретные.
- Рестартим машину, чтобы запустить все сервисы. Либо запускаем руками: `netfilter-persistent reload`, `systemctl restart openvpn@mgt`, `systemctl restart nginx`.

Сертификаты в Секретнице: [sec-01e5ahphpfw62mx8qvc5cszmx6](https://yav.yandex-team.ru/secret/sec-01e5ahphpfw62mx8qvc5cszmx6/explore/versions)
Текущая машинка: [mgt-proxy.sas.yp-c.yandex.net](https://qyp.yandex-team.ru/vm/sas/mgt-proxy)


## Как собрать образ для VM

Этот скрипт можно использовать для сборки образа виртуальной машины со всеми конфигами. Для этого:
- Клонируем самую свежую таску отсюда https://sandbox.yandex-team.ru/resources?page=1&pageCapacity=20&type=QEMU_IMAGE_SEARCH_XENIAL&attrs=%7B%7D&state=READY&attr_value=stable&owner=RCCS-ADMINS&attr_name=released
- В параметр "Setup scripts URLs" добавляем ссылку на setup_proxy.sh.
- Запускаем задачу.

Дальше получившимся образом можно налить виртуалку (искать в вики Qemu RTC).

Пример задачи: https://sandbox.yandex-team.ru/task/276952073/view


## Как диагностировать проблемы

Первичную диагностику проблем с проксёй можно произвести по инструкции https://wiki.yandex-team.ru/users/pedeathtrian/troubleshoot-mgt-proxy/
