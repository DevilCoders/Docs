
## Staging
### Описание
`Staging` (стейджинг) — совокупность систем программных вычислительных средств, целью которых является генерирование отдельный инстанс со слепком настоящих данных.  
Можно использовать в целях разработки и проверки отправляемого на merge request кода.

### Документация:
* [Описание 1](https://noc-gitlab.yandex-team.ru/nocdev/rt-docker#cli)
* [Описание 2](https://noc-gitlab.yandex-team.ru/nocdev/rt-docker/-/tree/master/noc/rttestctl)
* [Подключение БД стейджинга текущей ветки для локальной разработки](https://noc-gitlab.yandex-team.ru/nocdev/rt-docker/snippets/4)

### Ограничения
`Staging` не обладает доступом к сетевому оборудованию и внутренним системам Яндекса

### Пример использования
```bash
user@user-x:~# rttctl spawn
Creating env on n1.test.racktables.yandex-team.ru
[12.721882537s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: PHP-FPM not running. Waiting 5 seconds...
[18.288348542s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: PHP-FPM not running. Waiting 5 seconds...
[24.336673573s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: RTAPI not running. Waiting 5 seconds...
[29.991378693s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: RTAPI not running. Waiting 5 seconds...
[35.667784688s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: RTAPI not running. Waiting 5 seconds...
[41.172358285s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: RTAPI not running. Waiting 5 seconds...
[46.864202918s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: Alexandria not running. Waiting 5 seconds...
[52.496107792s] Current status 76cf2d31-7d58-4139-9b3d-1977dc0ba19a: Running.

user@user-x:~# rttctl ps
+-----+-----------------------------------------------------------------+-------------------+
| sas | n1.test.racktables.yandex-team.ru                               | dc=sas,weight=100 |
+-----+-----------------------------------------------------------------+-------------------+
| 1   | 76cf2d31-7d58-4139-9b3d-1977dc0ba19a                            | Running           |
|     | nocdev/racktables:master                                        |                   |
|     | until 2021-11-04 14:56:40                                       |                   |
|     | +0300 MSK (71h58m23.055865s) [                                  |                   |
|     | creator=user ]                                         |                   |
+-----+-----------------------------------------------------------------+-------------------+

user@user-x:~# rttctl ssh 76cf2d31-7d58-4139-9b3d-1977dc0ba19a
ssh -t -p 2222 n1.test.racktables.yandex-team.ru rt-fpm 76cf2d31-7d58-4139-9b3d-1977dc0ba19a 

user@user-x:~# rttctl mysql 76cf2d31-7d58-4139-9b3d-1977dc0ba19a
mysql -h n1.test.racktables.yandex-team.ru -u racktables -P 48655 -p***** racktables

user@user-x:~# rttctl rm 76cf2d31-7d58-4139-9b3d-1977dc0ba19a
Delete env 76cf2d31-7d58-4139-9b3d-1977dc0ba19a from node n1.test.racktables.yandex-team.ru
```
Исполняемые файлы и актуальную инструкцию по работе можно найти в **Документации** выше.