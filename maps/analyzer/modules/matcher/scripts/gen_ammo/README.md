#Скрипт генерации патронов для нагрузочного тестирования

Создает патроны для нагрузочного тестирования на основе сигналов из таблицы в YT.
Таблица должна иметь следующую структуру:
* uuid
* lon
* lat
* timestamp
* direction
* speed
* accuracy

##Входные параметры

|    |  Flag   |    Default | Description |
|--- |---      |---   |---|
| -t | --table |      | Путь к таблице с данными. Поддерживается YPath |
| -p | --proxy | hahn | YT proxy |
|    | --host  | dispatcher.maps.yandex.ru | Host для  http заголовка. Используйте matcher.maps.yandex.ru, если необходимо стрелять напрямую в матчер |
|    | --extra-params       |      |  Дополнительные параметры запроса: эксперименты и т.п. |

#Пример использования

```bash
./gen_ammo -t //home/maps/users/kor-den/signals-10000uids[#0:#200000] > ./dispatcher.ammo
```
