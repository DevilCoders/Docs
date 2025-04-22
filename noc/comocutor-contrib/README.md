### soft_modernizer.py
soft_modernizer.py устанавливается вместо с пакетом comocutor_contrib
```shell
soft_modernizer.py -h                                                                                                                                                                                            1:06
usage: soft_modernizer.py [-h] [-d] [--testing-fw] [-i] [-ftp FTP] [-n] [-o]
                          [-p]
                          HOSTS [HOSTS ...]

fw update

positional arguments:
  HOSTS             plain list of a hosts or racktables rack code

optional arguments:
  -h, --help        show this help message and exit
  -d, --debug       set logging on DEBUG
  --testing-fw      use testing fw
  -i, --info        set logging on INFO
  -ftp FTP          use this FTP server
  -n, --dry-run     dry run
  -o, --only-patch  only patch
  -p, --progress    show progress during downloading
```

### parsers
В этом репозитории хранятся функция для парсинга результаты CLI-команд таких как "display interface" и тесты этих функций.
Тесты нужны чтобы быть уверенным в том что последующие правках парсеров.

#### Последовательность добавления нового парсера
1. Создаем заготовоку для теста:
```bash
tests/make_test_case.py --host sas1-s763 --cmd "dis traffic-policy stat interface GE1/0/13" --outfile "vrp_traffic_policy_stat_iface"
```

2. Добавляем парсер в comocutor_contrib/parser.py. Фунция должна возвращать как можно данных с минимальными изменениями их формата.
3. Парсим данные лежащие в тесте полученном на первом этапе и записываем отпаршенные данные в этот тест. В строку ```result = None  # insert parsed result here```
3. Добавляем кортеж (\<function\>, \<outfile\>) в test/test_parsers.py
```python
CASES = (
    (parsers.parse_vrp_traffic_policy_stat_iface, "vrp_traffic_policy_stat_iface"),
```
