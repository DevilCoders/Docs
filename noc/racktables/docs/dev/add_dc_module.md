## Как добавить новый модуль DC
### Описание
Данное руководство призвано показать основные шаги для выполнения типовой задачи по добавлению модуля.
Мотивацией к написанию послужил тикет [NOCDEVDUTY-1094](https://st.yandex-team.ru/NOCDEVDUTY-1094).

### Задача
Существует более круная разновидность данной задачи - это добавление ДЦ.

Добавление модулей в Сасово и других ДЦ происходит чаще, и может выполняться дежурным NOCDEV.

### Шаги
* Проверить локацию в [боте](https://bot.yandex-team.ru/rsg/index.php)
* Уточнить, не нужны ли записи в [dynrows](https://racktables.yandex-team.ru/index.php?page=rackspace&tab=dynrows)
* Добавит запись в [bot-map.inc](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/plugins/bot-map.inc)
* [Создать](https://racktables.yandex-team.ru/index.php?page=tagtree&tab=edit) Tag локации, выбрав родительский

Если просят добавить в наливку:
* Опционально: добавить [vlandomain](https://racktables.yandex-team.ru/index.php?page=8021q) (не везде нужны vlandomain)
* Опционально: проверить и добавить ipv4pool/ipv6pool, если не подходят наливочные сети из соседней локации
* Добавить локацию в [ресурсы pns](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/plugins/pns-resources-dc.php)

> Switchdev не поддерживает работу с ipv6pool. При наличии выбора, pns отдаёт приоритет ipv6 против ipv4
