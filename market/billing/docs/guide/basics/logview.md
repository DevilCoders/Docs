# Logview

Logview - это сервера, которые позволяют разработчикам просматривать логи онлайн.

Типичная задача, с которой помогает справится logview - пришел запрос через балансер и надо посмотреть, на каком инстансе этот запрос выполнился.
Если бы не было logview, то пришлось по ssh залазить на каждый инстанс отдельно и там уже грепать логи.

Logview позволяет сделать grep из одного места сразу по всем инстансам.

## Как работает
### заходим на какую либо из машинок logview:
через балансер
```bash
$ ssh logview.market.yandex.net
```
### монтируем нужные нам инстансы (рассматривать будем на примере nanny и tpl биллинга)
Ищем в няне нужные нам сервисы: для этого идем в [сервисы няни](https://nanny.yandex-team.ru/ui/#/services) и в поле ввода вбиваем `tpl-billing`
![](https://jing.yandex-team.ru/files/andreybystrov/Screenshot%20from%202021-11-09%2011-43-56.png)
Видим 3 нужных прод сервиса - iva, sas и vla.

Открываем первый (например, iva) и в открывшейся вкладке копируем **название сервиса** - в данном случае это **production_market_tpl_billing_iva**
Тоже самое проделываем со всеми нужными (обычно, нужны все) инстансами

Далее на машинке logview есть специальный скрипт под названием `mount-service-log`, выполнять который надо с `sudo` правами.
Монтируем наши сервисы:
```bash
$ sudo mount-service-log -o remount production_market_tpl_billing_vla
Service: production_market_tpl_billing_vla
Folder /mnt/nanny/production_market_tpl_billing_vla/vla3-1734-702-vla-market-prod--f23-30098.gencfg-c.yandex.net has been umounted
Folder /mnt/nanny/production_market_tpl_billing_vla/vla3-1734-702-vla-market-prod--f23-30098.gencfg-c.yandex.net has been mounted
Folder /mnt/nanny/production_market_tpl_billing_vla/vla3-1766-044-vla-market-prod--f23-30098.gencfg-c.yandex.net has been umounted
Folder /mnt/nanny/production_market_tpl_billing_vla/vla3-1766-044-vla-market-prod--f23-30098.gencfg-c.yandex.net has been mounted

$ sudo mount-service-log -o remount production_market_tpl_billing_sas
Service: production_market_tpl_billing_sas
Folder /mnt/nanny/production_market_tpl_billing_sas/sas2-0428-c0b-sas-market-prod--559-24625.gencfg-c.yandex.net has been umounted
Folder /mnt/nanny/production_market_tpl_billing_sas/sas2-0428-c0b-sas-market-prod--559-24625.gencfg-c.yandex.net has been mounted
Folder /mnt/nanny/production_market_tpl_billing_sas/sas2-0076-76e-sas-market-prod--559-24625.gencfg-c.yandex.net has been umounted
Folder /mnt/nanny/production_market_tpl_billing_sas/sas2-0076-76e-sas-market-prod--559-24625.gencfg-c.yandex.net has been mounted

$ sudo mount-service-log -o remount production_market_tpl_billing_iva
Service: production_market_tpl_billing_iva
Folder /mnt/nanny/production_market_tpl_billing_iva/iva1-0510-4e3-iva-market-prod--c90-12569.gencfg-c.yandex.net has been umounted
Folder /mnt/nanny/production_market_tpl_billing_iva/iva1-0510-4e3-iva-market-prod--c90-12569.gencfg-c.yandex.net has been mounted
Folder /mnt/nanny/production_market_tpl_billing_iva/iva0-0444-iva-market-prod-tpl--c90-12569.gencfg-c.yandex.net has been umounted
Folder /mnt/nanny/production_market_tpl_billing_iva/iva0-0444-iva-market-prod-tpl--c90-12569.gencfg-c.yandex.net has been mounted
```

### Смотрим текущие логи
Теперь берем в руки grep и ищем нужную нам информацию **сразу во всех инстансах** (ищем строчку `End processing user shift partitions`):
```bash
andreybystrov@logview01hd:~$ grep --color=always 'End processing user shift partitions' /mnt/nanny/production_market_tpl_billing_{vla,sas,iva}/*/tpl-billing/tpl-billing.log
/mnt/nanny/production_market_tpl_billing_vla/vla3-1734-702-vla-market-prod--f23-30098.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 10:37:54,906] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-02
/mnt/nanny/production_market_tpl_billing_vla/vla3-1734-702-vla-market-prod--f23-30098.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 10:45:58,689] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-08
/mnt/nanny/production_market_tpl_billing_sas/sas2-0076-76e-sas-market-prod--559-24625.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 07:20:14,608] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-08
/mnt/nanny/production_market_tpl_billing_sas/sas2-0076-76e-sas-market-prod--559-24625.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 11:00:33,501] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-07
/mnt/nanny/production_market_tpl_billing_sas/sas2-0428-c0b-sas-market-prod--559-24625.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 11:07:33,400] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-04
/mnt/nanny/production_market_tpl_billing_iva/iva0-0444-iva-market-prod-tpl--c90-12569.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 10:45:26,080] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-01
/mnt/nanny/production_market_tpl_billing_iva/iva1-0510-4e3-iva-market-prod--c90-12569.gencfg-c.yandex.net/tpl-billing/tpl-billing.log:[2021-11-09 11:01:00,592] INFO  [queue-2-0] End processing user shift partitions for date 2021-11-05
```

Как видно, нашлось на всех инстансах за сегодня

(обрати внимание, что перечислены все cервисы {vla,sas,iva}, и искать надо во всех (обозначено *) инстансах)

### NB
можно завести скрипты, которые делают remount/grep на каком нибудь инстансе logview, и заходить сразу на него. Минус - если машинка выйдет из строя, то на нее не получиться попасть. Пример можно посмотреть тут (на примере того же tpl billing'a):
```bash
$ ssh logview01hd.market.yandex.net
andreybystrov@logview01hd:~$ cd /home/andreybystrov/
andreybystrov@logview01hd:~$ cat tpl_billing_mount 
sudo mount-service-log -o remount production_market_tpl_billing_vla
sudo mount-service-log -o remount production_market_tpl_billing_sas
sudo mount-service-log -o remount production_market_tpl_billing_iva
andreybystrov@logview01hd:~$ cat tpl_billing_grep 
str=$1
grep --color=always "$1" /mnt/nanny/production_market_tpl_billing_{vla,sas,iva}/*/tpl-billing/tpl-billing.log

```
Там будет и для тарифницы, и для тпл биллинга примеры с ремантом и грепом