# Руководство по сценарию "reserved-hosts-transfer"

Сценарий предназначен для выполнения быстрого ввода хостов из резервов в YP/Gencfg.
Резервы - хосты без нагрузки, существуют вне управления аллокаторов (например, хосты в [проекте](https://wall-e.yandex-team.ru/projects/hosts?project=rtc-reserve-mtn-sas))


Доступ к сценарию осуществляется через [IDM](https://idm.yandex-team.ru/#rf=1,rf-role=cTYH9Vus#walle/scenario/reserved-hosts-transfer(fields:()),f-status=all,sort-by=-updated,rf-expanded=cTYH9Vus)

## Ограничения
- адаптирован только к реалиям RTC (== сделаны с учетом всяких тонкостей относительно YP/Gencfg хостов)
- в данный момент невозможен отложенный старт сценария. При старте сценарий сразу приступает к разгрузке серверов через CMS в соответствии с пунктом данного документа "Ход работы сценария";
- также существуют общие лимиты на количество сценариев данного типа:
  * не более десяти активных сценариев типа **reserved-hosts-transfer** всего;

## Создание сценария
Создать сценарий можно на странице [Scenarios](https://wall-e.yandex-team.ru/scenarios). Нажимаем кнопку "Create", в появившейся форме в выпадающем списке "Scenario type" выбираем тип "reserved-hosts-transfer".
Заполняем форму:
- В поле "Ticket" указывает тикет в StarTrek'е, по которому проводятся работы. У робота [robot-walle@](https://staff.yandex-team.ru/robot-walle) должен быть доступ на чтение и создание комментариев в очереди StarTrek'а, или в этом конкретном тикете.
- В поле "Name" вводим произвольное осмысленное имя сценария.
- В поле "Project" вводим название проекта, в который нужно ввести хосты.
- В поле "Hosts" вводим список инвентарных номеров/fqnd'ов хостов, которые желаем перенести
- Установка галочки "Autostart" позволяет сразу же стартовать сценарий.

## Ход работы сценария
* Для начала проверяются лимиты:
  * не более десяти активных сценариев типа **reserved-hosts-transfer** всего
* Создается согласование на владельцев хостов.
* После получения аппрува хосты запрашиваются в CMS и отправляются в проект назначения, после чего при необходимости подготавливаются к работе (снова через CMS).
* В случае реджекта ждем решения оператора/владельца хостов/SRE/etc

## Работа через API
Список всех ручек API доступен по адресу https://api.wall-e.yandex-team.ru/

* создание:
  ```
  curl -X POST https://api.wall-e.yandex-team.ru/v1/scenarios \
    -d '{"name": "reserved hosts transfer test", "scenario_type": "reserved-hosts-transfer", "ticket_key": "TICKET-66", "hosts": ["host1.yandex-team.ru", "host2.yandex-team.ru"], "script_args": {"target_project": "some-project-id"}}' \
    -H 'Content-Type: application/json' -H 'Authorization: OAuth <token>'
  ```
