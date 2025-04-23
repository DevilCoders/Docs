# Инструкции и скрипты дежурной смены

## Скрипты

- [Скрипт для раскладывания обновлений софта на huawei](https://noc-gitlab.yandex-team.ru/nocdev/comocutor-contrib/-/tree/master/utils)
- [Скрипт для массовой рассылки уведомлений о работах на свитчах](https://noc-gitlab.yandex-team.ru/nocdev/automation/blob/master/other/duty_email_notifications.py)
- [Скрипт для плановой перезагрузки свитчей Huawei](https://noc-gitlab.yandex-team.ru/nocdev/automation/blob/master/other/scheduler_reboot_hw_sw.py)
- [Планирование обновлений на Nexus](https://noc-gitlab.yandex-team.ru/darkyman/nexus_schedule_upgrade/blob/master/schedule.py)
- [Скрипт для массовой замены ip управления на Huawei CE L3Tor](https://noc-gitlab.yandex-team.ru/nocdev/automation/blob/88f8ba8ad3f38ef9f9857dbd288c06eb01e4fbb4/other/change_me_huawei_tor_new.py)
- [Скрипт для нарезки стандартного набора офисных сетей](https://noc-gitlab.yandex-team.ru/nocdev/automation/blob/master/other/create_office_subnets.py)

## Офисная сеть

- [Получение замена сертификатов для офисных серверов](/nocdoc/office/manuals/office_server_cert_update/about)
- [снятие трафика со стыка офис<->бордер](/nocdoc/dc/manuals/drain_dc_office/about)
- [Wiki: общая страница офисных сетей с информацией по каждому офису](https://wiki.yandex-team.ru/noc/Office/)
- [Wiki: сводная по контактам операторов для региональных офисов](https://wiki.yandex-team.ru/users/onadtochiy/ofisy/Uslugi-svjazi/)
- [подготовка, настройка и эксплуатация офисных маршрутизаторов](/nocdoc/office/manuals/common_info/about)
- [замена диска](/nocdoc/duty/manuals/hddreplace/about)
- [Wiki: переход с HDD на SSD](https://wiki.yandex-team.ru/borislytochkin/4kzfs/)
- [выделение новых сетей для офиса](nocdoc/dc/manuals/ipv4/howto_get_office_nets/about)
- [немного об ipmi](/nocdoc/office/manuals/oobm/about)
- [команды ipmi](/nocdoc/office/manuals/ipmi_commands/about)
- [смена адресов операторов и внешних адресов для тунелей](/nocdoc/office/manuals/ipsec_change_external_igb_ip/about)
- [смена внутренних адресов для ipsec](/nocdoc/office/manuals/ipsec_change_internal_ip/about)
- [смена адресов dc-ix](/nocdoc/office/manuals/dc_ix_change_ip/about)
- [наливка роутера FreeBSD](/nocdoc/office/manuals/freebsd_installation/about)
- [Wiki: Восстановление конфига Cisco из бэкапа](https://wiki.yandex-team.ru/users/karpovpn/vosstanovlenie-konfiga-cisco-iz-bjekapa/)
- [Ввод в эксплуатацию пользовательского коммутатора](/nocdoc/office/manuals/access_sw_install/about)
- [Wiki: Ввод в эксплуатацию  Autonomous WiFi точки доступа](https://wiki.yandex-team.ru/noc/office/wifi/cisco-wds/)
- [Ввод в эксплуатацию ТД ARUBA](/nocdoc/office/manuals/aruba_ap_connection/about)

## Телефония

- [Инструкции для nocduty от Влада](https://wiki.yandex-team.ru/VladislavBalva/ChtoDelatPriZazhiganiiProverok/)

## Управление трафиком

[Описание типовых проблем и методы их решения](/nocdoc/trafficmgmt/manuals/main_problems/about)
[Блокировка DDoS на сервисы на уровне сети](/nocdoc/trafficmgmt/manuals/syn_flood_blocking/about)

## Обслуживание и эксплуатация сервисной сети в ДЦ

- [Обновление программного обеспечения коммутаторов](/nocdoc/dc/manuals/switch_software_update/about)
- [Снятие трафика между spine свитчами](/nocdoc/dc/manuals/drain_spines/about)
- [Wiki: Разбор пиринга на бордере](https://wiki.yandex-team.ru/users/karpovpn/Razbor-piringa-na-bordere/)
- [Снятие трафика с пира](/nocdoc/dc/manuals/drain_peer/about)
- [Wiki: Cumulus Linux Mellanox](https://wiki.yandex-team.ru/users/karpovpn/Cumulus-Linux-Mellanox/)
- [Wiki: noc-ck-cli](https://wiki.yandex-team.ru/users/karpovpn/noc-ck-cli/)
- [Wiki: annushka](https://wiki.yandex-team.ru/users/karpovpn/annushka/)
- [Wiki: Замена L3ToR с Huawei на Cumulus](https://wiki.yandex-team.ru/users/smarochkin/Zamena-L3ToR-s-Huawei-na-Cumulus/)
- [Организация ipv4 для ipv6-only серверов](/nocdoc/dc/manuals/IPv6to4/about)
- [Порядок выделения tun64 сетей](/nocdoc/dc/manuals/tun64newnet/about)
- [Wiki: etherchannel или как правильно расширять аплинк](https://wiki.yandex-team.ru/noc/duty/swc/)
- [Инструкция по работе с HMC-ошибками](/nocdoc/dc/manuals/how_to_handle_hmc_errors/about)
- [Обращение в техническую поддержку вендора](/nocdoc/dc/manuals/escalation/about)
- [Mellanox how to create the RMA](/nocdoc/dc/manuals/mellanox_how_to_create_rma/about)
- [Wiki: Установка оборудования](https://wiki.yandex-team.ru/dc/doc/install/)

## Магистральная сеть и зоны ответственности операторов

- [Регламент доступа в защищенные стойки точек усиления (коллокейшн](https://wiki.yandex-team.ru/security/physec/Reglament-dostupa-v-zashhishhennye-stojjki-tochek-usilenija/)
- [МСК <-> ДЦ Сасово](https://wiki.yandex-team.ru/noc/sasovo/)
- [МСК <-> ДЦ Владимир](https://wiki.yandex-team.ru/NOC/Vladimir/)
- [Collocations](https://wiki.yandex-team.ru/devnet/Collo/)

## Общее

- [Регламент реагирования на проблемы HBF](https://wiki.yandex-team.ru/noc/reglament-reagirovanija-na-problemy-hbf/?from=%252Fusers%252Fm-arefiev%252FReglament-reagirovanija-na-problemy-HBF%252F)
- [Диагностика сетевых проблем](https://wiki.yandex-team.ru/NOC/troubleshooting/)
- [Наиболее часто задаваемые вопросы при обращении в NOC](https://wiki.yandex-team.ru/noc/faq/)
- [Инструкция по обращениям по владению сетевыми ресурсами](https://wiki.yandex-team.ru/users/m-arefiev/instrukcija-po-obrashhenijam-po-vladeniju-setevymi-resursami/)
- [Дежурные RTC](https://abc.yandex-team.ru/services/routineoperations/duty/)
- [Календарь дежурств YT](https://calendar.yandex-team.ru/embed/week?embed&layer_ids=42060&tz_id=Europe%2FMoscow&uid=1120000000000720)

