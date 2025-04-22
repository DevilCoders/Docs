## Закрыть ДЦ
Закрытие ДЦ делается в два этапа:
 - закрытие балансера в ДЦ
 - закрытие бекендов в ДЦ

### закрытие балансера
Делается при помощи ручек в [ITS](https://wiki.yandex-team.ru/awacs/tutorial/its/):
 - ищем внизу нужную локацию среди вкладок внизу экрана,
 - жмем `[Apply]` в разделе `balancer/tavern_production_mail_yandex_net/XXX/XXX`  https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tavern.production.mail.yandex.net/its/ .


Нужно иметь ввиду что [ITS](https://wiki.yandex-team.ru/awacs/tutorial/its/) на баланcере настрен таким образом, чтобы таверна участвовала в "общих ученьках". Это значит что не нужно закрывать ДЦ руками при "общих ученьках".

### закрытие бекендов
Делается при помощи весов балансировки по локациям – https://nanny.yandex-team.ru/ui/#/l7heavy/tavern.production.mail.yandex.net. Документаци по управлению весами – https://wiki.yandex-team.ru/awacs/tutorial/l7heavy/

Веса так же меняются при "общих ученьках" командой общей доступности.
