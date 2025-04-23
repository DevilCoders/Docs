# BGP Фильтры

## Назначение
Проверяет и обновляет `prefix-list`ы на бордерах

## Управление поведением
### Теги


### Настройки
Используется на оборудовании по предикатам в Permissions:
 - [работает проверка Yandex PLs]: Причем тут работает только для Juniper
 - [работает генерация bgp-pl]: тут работает для Juniper, Quagga, Bird

### Cron
Запускается по крону. Частоту искать в scripts/update-rt-crontab.sh по ключевым словам:
 - bgpPLQueueMaker
 - bgpPLQueueExec
 - checkInnerPLs

### Release Notes
#### 10.2021 
- Пределано определение девайсов на breed
- Добавлена поддержка Juniper PTX по breed
- Упразднена поддержка Quagga