# HRDigital: ticketsSummoneer
Система автоматизации призывания руководителей в тикеты очереди найма

## Разработка
Для каждого департамента в каталоге processors можем существовать свой файл
с классом для обработки workflow данного департамента.

Поскольку тикеты лежат в трекере и не содержат всех необходимых комментариев от необходимых
глав, то единственный нормальный способ отлаживать это - через тесты.
К тому же, из-за ветвистости логики так получается гораздо надежнее вносить правки.

### Задампить контент тикета и его департамент
```bash
# TICKET_ID - идентификатор тикета вида: MARKETJOBTEST-20
python exec.py dump --ticket <TICKET_ID> 
```
В результате выполнения данной команды в processors/data появится json-файл
с данными тикета и отдельно json-файл с данными департамента.

### Прогнать все тесты
```bash
./test_all.sh
```

### TODO
Я не разрабатывал этот код с нуля и не особо работал с python-ом, так что не ругайте за то, что как это написано (изначальная версия сохранена в old.py).
Я постарался сделать так, чтобы этот код было проще отлаживать и сложнее поломать.
Надеюсь, мне это отчасти удалось. Осталось еще немало работы.
 - выделить сущность parser из main  
 - оптимизировать процесс парсинга  
 - структурировать и дописать тесты  
 - перевести код на Python3, добавить типы  
 - переработать подход работы с департаментами (выделить отдельный класс для департамента и добавить ему методы)  


## Работа в production
TicketsSummoneer состоит из двух частей:
 - sandbox-таск, лежит по адресу: arcadia/sandbox/projects/market/ticketsSummoneer
 - python-собираемый бинарник - лежит по адресу: arcadia/market/tools/tickets_summoneer

1) Sandbox-таск просто правится, код пушится в arc, проходит проверки, разъезжается по инстансам sandbox (это может занимать значительное время) и готов к работе.
Для запуска требует наличия в vault sandbox-а пары токенов, а также собранный бинарный таск.  

2) Бинарник необходимо собирать внутри Sandbox-а с помощью таска MARKET_YA_MAKE.
Этот таск запускается вручную. !ВАЖНО! после копирования и перед запуском необходимо обязательно перепроверять номер ревизии,
который указывается в поле "svn url for arcadia".  

3) Скрипт должен висеть в sandbox в schedule и запускаться по расписанию раз в час.  

Скрипт в бою ходит в wiki и staff от этого приложения* https://oauth.yandex-team.ru/client/7724aab7091b4db9b82c1e0140eb5ded  
Токены получались от имено робота robot-market-hire  
Здесь доменный пароль от робота: https://yav.yandex-team.ru/secret/sec-01d6bbsbeadzhdd047hdbxtt8v/explore/versions  
Токены лежат в sandbox-vault под названиями: MARKET_TICKETS_SUMMONEER_TRACKER_TOKEN_prod и MARKET_TICKETS_SUMMONEER_STAFF_TOKEN_prod  


### Для просмотра в браузере структуры департамента, можно использовать url:
```
https://api.staff.yandex-team.ru/v3/groups?_one=1&url=<ПОДСТАВИТЬ_СЮДА_ID_ДЕПАРТАМЕНТА>&_fields=level,department.heads.role,department.heads.id,department.heads.person,department.heads.login,ancestors.level,ancestors.department.heads.role,ancestors.department.heads.login,ancestors.department.heads.id,ancestors.department.heads.person.name,ancestors.department.heads.person.login
```

### Полезная информация по работе с Sandbox
[Грабли Sandbox](https://wiki.yandex-team.ru/users/alexahdp/sandbox-my-manual/)  
