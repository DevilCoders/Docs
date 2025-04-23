## Y.Deploy

Группа tycoon-www в Y.Deploy – https://deploy.yandex-team.ru/projects/tycoon-www

### Основные стейджы:

* [Production](https://deploy.yandex-team.ru/stages/tycoon-www-production)
* [Prestable](https://deploy.yandex-team.ru/stages/tycoon-www-prestable)
* [Testing](https://deploy.yandex-team.ru/stages/tycoon-www-testing)

### Production балансер

Запросы с `yandex.{tld}` распределяют следующие `knoss_fast` апстримы:
* [/sprav](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast/upstreams/list/sprav/show/)
* [/rehber](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast/upstreams/list/rehber/show/)
* [/directory](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast/upstreams/list/directory/show/)

Дальше запросы попадают в L7-балансеры в соответсвующих локациях (MAN, SAS, VLA). [Namespace в Nanny](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-production.sprav.yandex.ru/show/)

Смотреть за кол-вом запросов, таймингами, ошибками можно в [мониторинге неймспейса](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=tycoon-www-production.sprav.yandex.ru;itype=balancer;ctype=prod;locations=man,sas,vla;prj=tycoon-www-production.sprav.yandex.ru;signal=tycoon-www-production_sprav_yandex_ru;)

За обработку входящих запросов (в какой бекенд направить запрос) отвечают [апстримы](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-production.sprav.yandex.ru/upstreams/list/). На очередность их срабатывания влияет параметр label `order`. Например, `0001` сработает раньше `0010`. В каждом апстриме можно настроить условие по которому он отработает, таймауты, ретраи и т.д.

[Основной апстрим](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-production.sprav.yandex.ru/upstreams/list/tycoon-www-production_sprav_yandex_ru/show/) отвечает за распределение запросов в контейнеры с нашим приложением. Остальные апстримы (`profile-proxy`, `support-poxy` и т.д.) проксируют запросы в другие бекенды. Например, с `yandex.{tld}/sprav/support` нужно перенаправлять запрос в другой бекенд и показывать документацию.

### Алерты

* [5xx ошибки](https://yasm.yandex-team.ru/alert/tycoon-server-errors)
* [4xx ошибки](https://yasm.yandex-team.ru/alert/tycoon-server-4xx-errors)

### Testing балансер

Запросы с `l7test.yandex.{tld}` распределяют следующие `knoss_fast_testing` апстримы:
* [/sprav](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/upstreams/list/sprav/show/)
* [/rehber](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/upstreams/list/rehber/show/)
* [/directory](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/upstreams/list/directory/show/)

[Namespace в Nanny](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-testing.sprav.yandex.ru/show/)

[Апстримы](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-testing.sprav.yandex.ru/upstreams/list/)

[Основной апстрим](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-testing.sprav.yandex.ru/upstreams/list/main_main/show/)

### Prestable балансер

Тут у нас собственный L3-балансер. Он принимает запросы с `tycoon-www-prestable.sprav.yandex.ru` и направляет их в L7-балансеры и дальше стандартно:

[Namespace в Nanny](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-prestable.sprav.yandex.ru/show/)

[Апстримы](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-prestable.sprav.yandex.ru/upstreams/list/)

[Основной апстрим](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tycoon-www-prestable.sprav.yandex.ru/upstreams/list/tycoon-www-prestable_sprav_yandex_ru/show/)
