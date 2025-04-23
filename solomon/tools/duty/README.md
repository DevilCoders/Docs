# Utility to manage Solomon duty schedule

Build utility first

```
$ ya make -r
```

## 1. Show who is on duty today

Will print who is responsible today for each duty schedule.

```
$ ./duty who

Поддержка пользователей
    name: Samar Chokutaev
  e-mail: samarius@yandex-team.ru
   phone: +7 916 361-44-53
      tg: https://telegram.me/samarius

Инцидент менеджмент
    name: Andrey Guschin
  e-mail: guschin@yandex-team.ru
   phone: +7 925 781-71-24
      tg: https://telegram.me/guschin

SRE
    name: Konstantin Balakirev
  e-mail: kbalakirev@yandex-team.ru
   phone: +7 953 412-63-16
      tg: https://telegram.me/kvbalakirev

UI
    name: Artem Luchin
  e-mail: kloof@yandex-team.ru
   phone: +7 916 859-08-08
      tg: https://telegram.me/artem_luchin
```

## 2. Update duty schedule in Yandex.Cloud resps

Yandex.Cloud manages duty schedules in separate [git repository](https://bb.yandex-team.ru/projects/CLOUD/repos/resps/browse).

Our schedule is located in file [cvs/yc_solomon.csv](https://bb.yandex-team.ru/projects/CLOUD/repos/resps/browse/cvs/yc_solomon.csv).

To update this file just run following command and utility will autotically clones repository, modifies appropriate file, commits it and pushs changes back to an upstream repository:

```
$ ./duty update
2021/08/09 12:55:29 cloning repository https://bb.yandex-team.ru/projects/CLOUD/repos/resps
2021/08/09 12:55:30 reading previous schedule from cvs/yc_solomon.csv
2021/08/09 12:55:30 generating new schedule
2021/08/09 12:55:30 writing new schedule to cvs/yc_solomon.csv
2021/08/09 12:55:30 committing schedule changes
2021/08/09 12:55:30 hash af32e54c51e6f79d761db60aa9369a4aa57f0fc9
2021/08/09 12:55:30 pushing changes to remote repository
2021/08/09 12:55:31 see commit at https://bb.yandex-team.ru/projects/CLOUD/repos/resps/commits/af32e54c51e6f79d761db60aa9369a4aa57f0fc9
```
