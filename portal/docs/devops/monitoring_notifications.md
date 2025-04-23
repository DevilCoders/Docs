# Оповещения
Каждая портальная проверка должна иметь тег срочности. Для каждого тега определен свой сценарий оповещений.

{% note tip "" %}

Во время большого факапа, чтобы перестать получать отвлкающие от тушения пожара звонки, можно поставить [mute](https://docs.yandex-team.ru/juggler/notifications/mutes) на все портальные проверки используя селектор `namespace=portal` с адекватным временем till. После тушения пожара нужно не забыть снять мьют.

{% endnote %}

## Продуктовые оповещения
Тег | Звоноки днем <br>(через)</br> | Звоноки ночью <br>(через)</br> | Telegram | Описание
:--- | :---: | :---: | :---: | :---
<span style="color: green;">morda-product-information</span> | **-** | **-** | **-** | Проверки светятся только на [панели дежурного в Juggler](https://juggler.yandex-team.ru/dashboards/d6c567f4) и нужны для понимания ситуации в целом. Оперативная работа по ним ведется в рабочее время. Влияния на пользователей нет. Примеры: поломки тестов, девов.
<span style="color: #e8a202;">morda-product-warning</span> | - | - | [+](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug) | Оперативная работа по ним ведется в рабочее время, но желательно сильно не откладывать. Влияния на пользователей нет. Примеры: заканчивается место в elasticsearch сервиса portal-kibana; сломались бекапы MADM.
<span style="color: red;">morda-product-critical</span> | [5 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=60520d960e7999ae6a829144) | [10 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=605c589825ed532c63a11084) | [+](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug) | Класс проверок, сигнализирующих о деградации качества сервиса (или о риске критической деградации). Примеры: инфраструктурные проверки (CPU, память, диск, etc.); поломки подисточников.
<span style="color: #520606;">morda-product-disaster</span> | [0 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=605deac67029e42408bc3041) | [5 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=605dea874ba09764087fdb37)| [+](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug) | Нужно бежать и чинить. Примеры: ошибки Морды; 4xx статики Морды; аппхостовые фейлы.
<span style="color: #2b0000;">morda-product-horror</span> | [0 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id%3D6112bbca12eded70bd2fb3af%7Crule_id%3D6102af8a1cafd7c728e746c4)<sup>*</sup> | [0 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id%3D6102b06f26b13a11d79e4af0%7Crule_id%3D6102af8a1cafd7c728e746c4)<sup>*</sup> | [+](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug) | **<u>Всем</u>** нужно бежать и чинить. Примеры: тыквы; падение трафика ниже критического уровня; загорелись активные HTTP проверки на yandex.tld.
<sup>*</sup> Звонок дежурному первой очереди + звонок SRE

## Оповещения Платформы 
Тег | Звоноки днем <br>(через)</br> | Звоноки ночью <br>(через)</br> | Telegram | Описание
:--- | :---: | :---: | :---: | :---
<span style="color: green;">morda-platform-information</span> | **-** | **-** | **-** |
<span style="color: #e8a202;">morda-platform-warning</span> | [10 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=60eed77cd0b11fca26a23c7e&project=portal) | - | [+](https://t.me/joinchat/BlyRegsiusIHkvRRW8y7Ug) | 
<span style="color: red;">morda-platform-critical</span> | [5 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=60eed7e8ba4c5d9538958e94) | [10 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=60eed839257b28624617eada) | [+](https://t.me/joinchat/UdBbeXWuF8xjM2Qy) | 
<span style="color: #520606;">morda-platform-disaster</span> | [0 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=60eee43cba4c5d9538958e95) | [5 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=60eee470c85ad1e6117802a3)| [+](https://t.me/joinchat/UdBbeXWuF8xjM2Qy) |
<span style="color: #2b0000;">morda-platform-horror</span> | [0 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id%3D6102b64b8f7c801fb8c350a1%7Crule_id%3D6112bbca12eded70bd2fb3af)<sup>*</sup> | [0 минут](https://juggler.yandex-team.ru/notification_rules/?query=rule_id%3D6102b64b8f7c801fb8c350a1%7Crule_id%3D6102b06f26b13a11d79e4af0)<sup>*</sup> | [+](https://t.me/joinchat/UdBbeXWuF8xjM2Qy) |
<sup>*</sup> Звонок дежурному первой очереди + звонок SRE
