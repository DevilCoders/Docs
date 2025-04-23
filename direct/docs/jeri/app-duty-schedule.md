# Планирование дежурства app-duty в abc (УСТАРЕЛО)

## Что где { #theory }

Дежурство в abc: <https://abc.yandex-team.ru/services/direct/duty/?role=3212>
Смены по 1 дню, т.к. abc (пока) не умеет неравномерное расписание (3/4 дня).

id дежурства: `3212`, можно увидеть через скрипт, см. ниже.

Заполняем расписание скриптом `dt-app-duty-manage-shifts.py` по текстовому описанию.
Скрипт и данные лежат здесь: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/duty-tools>

Скрипт ожидает oauth-токен для abc в файле `~/.abc-auth-token`, по параметру может брать другой файл.

Посмотреть id дежурств в сервисе direct:
```
direct-utils/duty-tools$ bin/dt-app-duty-manage-shifts.py --list
(3212) direct-app-duty2
```

## Заполнить новую итерацию дежурства { #new-schedule }

Идем в рабочую копию `direct-utils/duty-tools`.

В каталог `data` кладем новый текстовый файл с расписанием или продолжаем старый.

Пример:

```
$ head -n 4 data/direct-app-duty-2020.shifts.txt
2020-11-16 4-7 gukserg@ mspirit@
2020-11-23 1-3 elwood@ andreypav@
2020-11-23 4-7 snirinn@ kalchevskaya@ # комментарий
2020-11-30 1-3 adubinkin@ robot-direct-admin@
```

Формат:
- дата начала недели
- дни недели, попадающие в дежурство ( `1-3` = понедельник-среда, `4-7` = четверг-воскресенье )
- логины первого и второго дежурного
- в конце строки можно комментарий после `#`
- в качестве плейсхолдера для неназначенных смен используем робота `robot-direct-admin`

Запускаем запись, пример:

```
./bin/dt-app-duty-manage-shifts.py -s direct-app-duty2 -f 2020-11-23 -t 2020-12-15 --assign-shifts --shifts-file data/direct-app-duty-2020.shifts.txt
```

Диапазон дат (`-f`, `-t`) поменять на нужный, файл с расписанием (`--shifts-file`) по необходимости тоже.

Если скрипт падает с таймаутами или 500-ми ошибками от API abc, повторяем запуск. Можно с меньшим диапазоном дат.

Результат проверяем в интерфейсе abc: <https://abc.yandex-team.ru/services/direct/duty/?role=3212>

## За чем следим при планировании дежурств { #invariants }

- за один цикл дежурства у одного апп-дьюти две смены
- одна смена в начале недели, одна &mdash; в конце
- одна смена первым дежурным, одна &mdash; вторым

## Ссылки { #links }

- Дежурство в abc: <https://abc.yandex-team.ru/services/direct/duty/?role=3212>
- Инструменты: <https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/duty-tools>
- Робот `robot-direct-admin` на стаффе: <https://staff.yandex-team.ru/robot-direct-admin>
