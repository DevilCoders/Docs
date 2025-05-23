# Пароль на девайс
Девайсы на SoC Amlogic имеют вшитый ROM загрузчик, который стартует по сигналу
на boot5 линии. Он позволяет читать и писать разделы на устройстве, что в
свою очередь может открыть доступ (в том числе эксплойтить известную
уязвимость) для злоумышленников.

Чтобы ограничить доступ к этому функционалу этот загрузчик имеет
возможность установить пароль на USB и/или JTAG. Если устройство
защищено этим паролем, то перед тем, как читать/писать в память
необходимо предоставить этот пароль.

Пароль представляет из себя массив размером не более 16 байт.

## Пароль на Yandexmodule2
Для `yandexmodule2` было принято решение генерировать и прошивать на
фабрике уникальные пароли на каждый девайс.

Пароли доставляются из базы данных Jangles в YT с помощью специальной
sandbox таски -
[arcadia/sandbox/projects/quasar/fetch_jangles_passwords](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/quasar/fetch_jangles_passwords). При этом пароли сперва шифруются ассиметричным шифрованием и в том числе в YT лежат в зашифрованном виде.

> Чтобы получить доступ к ключу для расшифровки следует запросить доступ на чтение соотвествующего секрета в YAV! Иначе скрипт не позволит вам расшифровать пароль!

## Запрос пароля
Если все доступы есть, то для получения пароля необходимо узнать
идентификатор вашего устройства и передать его скрипту через один
из параметров. Подробнее про параметры скрипта можно узнать
```Bash
./aml_password --help
```

Получить идентфикатор устройства и использовать пароль для перепрошивки
можно с помощью утилиты
[arcadia/smart_devices/tools/aml_tool](https://a.yandex-team.ru/arc/trunk/arcadia/smart_devices/tools/aml_tool).

## Сборка

### Linux
```Bash
ya make
```

### Mac
```Bash
ya make --use-clonfile
```
