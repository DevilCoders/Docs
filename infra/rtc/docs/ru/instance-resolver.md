# Instance Resolver
UI расположен по адресу [instance-resolver.in.yandex-team.ru](https://instance-resolver.in.yandex-team.ru).

API / документация по нему расположены по адресу [instance-resolver-api.in.yandex-team.ru](https://instance-resolver-api.in.yandex-team.ru).

Информацию о проекте можно найти в [аркадии](https://a.yandex-team.ru/projects/rtc_instance_resolver/).

Для доступа к сервису нужно заказывать дырки до `_RTC_INSTANCE_RESOLVER_NETS_`, для аутентификации используется TVM. Не стоит заказывать доступ до `instance-resolver-api.in.yandex-team.ru`, т.к. используется DNS балансер.

## Почему вы получили уведомление {#why}
На хостах, где сейчас проводятся работы размещены контейнеры сервисов / виртуальных машин для которых ваш логин или группа, в которой вы состоите, указаны во владельцах сервиса.

### Nanny
В Nanny для поиска ответственных используется ABC сервис, указанный на вкладке `General Info`. Из сервиса берутся все участники с ролями `administration` и `devops`. Если ABC сервис не указан или же пользователей с нужной ролью не найдено, то берутся логины и группы из поля `Service owners`. Если группа является ABC сервисом, то опять участники фильтруются по соответствующим ролям.
![2020-05-08_12-41-26.png](https://jing.yandex-team.ru/files/dldmitry/2020-05-08_12-41-26.png =150x249)
![2020-05-08_12-33-21.png](https://jing.yandex-team.ru/files/dldmitry/2020-05-08_12-33-21.png =600x77)

Для включения / выключения отправки нотификаций можно воспользоваться `Maintenance notifications`:
![2020-05-08_12-46-07.png](https://jing.yandex-team.ru/files/dldmitry/2020-05-08_12-46-07.png =400x85)

По умолчанию считается что нотификации выключены.

### Qloud
Для Qloud берутся все пользователи и группы сервиса с любыми правами, кроме глобальных пользователей и групп сегмента.

### QYP
Для QYP используются владельцы виртуальной машины.

### Deploy
!!TBD!!

### Ошибочное уведомление, отказ от уведомлений
Если вы проверили, что не входите в список ответственных за сервис и получили сообщение об ошибке - напишите автору рассылки.

Если вы хотите никогда не получать уведомления о работах на хостах RTC - напишите автору рассылки.

## Клиенты сервиса
* [Overseer](https://wiki.yandex-team.ru/noc/overseer/), например, [vla1-1s134](https://overseer.common-int.yandex-team.ru/html/interested_by_rtc_switch?host=vla1-1s134&user=__auto__)
* [notifyctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/rtc/notifyctl)

