# convert-to-unique-events-recount-requests

Утилита конвертирования рекаунт-реквестов из формата двух связанных таблиц events/deduplicated_hashes в unique_events. Исходные рекаунт-реквесты получаются дампом из интерфейса [Zooface](https://z.mtrs.yandex-team.ru). Считается, что они сжаты gzip. Выходные создаются без сжатия, пригодные для вставки через интерфейс Zooface.

```
drobus@drobus:~$ ~/arc/metrika/core/utils/recount-requests/convert-to-unique-events/convert-to-unique-events-recount-requests --help
usage: convert-to-unique-events-recount-requests [-h]
                                                 [-v [{info,information,warn,warning,critical,error,debug,fatal}]]
                                                 -i INPUT_PATH -o OUTPUT_PATH

optional arguments:
  -h, --help            show this help message and exit
  -v [{info,information,warn,warning,critical,error,debug,fatal}], --verbose [{info,information,warn,warning,critical,error,debug,fatal}]
                        verbose level
  -i INPUT_PATH, --input_path INPUT_PATH
                        Path with events/deduplicated_hashes recount requests
  -o OUTPUT_PATH, --output_path OUTPUT_PATH
                        Path for unique_events recount requests

For example ./convert-to-unique-events-recount-requests -i ~/rr/in -o ~/rr/out
```
