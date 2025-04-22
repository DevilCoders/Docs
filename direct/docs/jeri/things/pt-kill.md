# pt-kill

Самое главное, что надо знать о **pt-kill**.

**pt-kill** -- инструмент для отстрела медленных запросов, входящий в набор [percona toolkit](https://www.percona.com/doc/percona-toolkit/LATEST/pt-kill.html).

В проде запущен на хостах [%direct_myql](https://c.yandex-team.ru/groups/direct_mysql)

{% cut "Как проверить, что запущен и посмотреть с какими параметрами" %}

Через [executor](./executer)
```
[Serial] yourlogin> exec %direct_mysql ps a -C 'perl'|grep -v grep|grep pt-kill
```

{% endcut %}

### Что делает:

- подключается к mysql, следит за активными запросами (SHOW PROCESSLIST)
- если находит запросы, попадающие под заданные параметрами критерии отстрела - завешает их

[Лог завершенных запросов](https://direct.yandex.ru/logviewer#~(logType~'mysql_ptkill~form~(fields~(~'log_time~'hostname~'query_id~'request_time~'query~'meta~'instance)~conditions~()~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Дополнительная информация

Документация: <https://www.percona.com/doc/percona-toolkit/LATEST/pt-kill.html>

{% cut "Как проверить, что работает" %}

```
#Запрос должен длиться 60 секунд, но завершается через 30
$ time dbs-sql pr:ppc:5 'select sleep(60) /*  pt-kill-me  */'
pr:ppc:5
+-----------+
| sleep(60) |
+-----------+
|         1 |
+-----------+

real    0m38.936s

#Контрольный запрос для проверки
$ time dbs-sql pr:ppc:5 'select sleep(60) /*  pt-no-kill-me  */'
pr:ppc:5
+-----------+
| sleep(60) |
+-----------+
|         0 |
+-----------+

real    1m0.232s
```

{% endcut %}

Пакеты
- [percona-toolkit](https://www.percona.com/doc/percona-toolkit/LATEST/installation.html)
- [yandex-du-ptkill-ppcdata](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/yandex-du-ptkill-ppcdata) - директ-специфичная часть

На хостах запускается/останавливается через sv.

{% cut "Как pt-kill определяет какие запросы убить" %}

Вывод SHOW PROCESSLIST фильтруется через набор пар ```регулярное выражение, таймаут```, заданных в ```/etc/ptkill/ppcdata.pl```.
Если находится соответствие по телу запроса, и время его выполнения больше заданного для подобных запросов таймаута - он проходит через фильтр.
Запросы, для которых не нашлось соответствия, через фильтр не проходят и pt-kill не будет их завершать.

Если запрос прошел фильтр - время его выполнения сравнивается со значением, заданным параметром ```--busy-time``` (30).
Запросы, выполняющиеся дольше ```busy-time``` завершаются.

Подробнее см. [/etc/ptkill/ppcdata.pl](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/yandex-du-ptkill-ppcdata/etc/ptkill/ppcdata.pl) и [документацию](https://www.percona.com/doc/percona-toolkit/LATEST/pt-kill.html).

{% endcut %}

### Отстрел запросов от конкретного оператора

**Этот режим предназначен для использования в чрезвычайных ситуациях, когда ухудшение качества работы сервиса неизбежно. Если сомневаешься - посоветуйся с опытным коллегой.**

**Интерфейс инструмента оставляет желать лучшего и может меняться. Если надо сделать снова, не полагайся на память, прочитай ещё раз документацию.**

**При включении прибивалки на оператора заводите тикет на отложенное действие на выключение, чтобы не потерять!**

Мотивация: иногда пользователь (обычно агентство с большим количеством клиентов в одном шарде) начинает задавать много одновременных запросов в mysql и mysql не справляется с нагрузкой (вплоть до падения сервера по OOM). В этом случае можно локализовать ущерб, отстреливая запросы этого пользователя, контролируя, что их не выполняется слишком много одновременно. По-хорошему, такое ограничение должно реализовываться в коде приложения, но сейчас этого нет.

Как это отличается от штатного режима pt-kill:
- отстреливаются запросы не по времени выполнения, а по оператору (содержащейся строке `operator=<...>`)
- короче интервал
- прибиваются не все запросы, а только самые новые, чтобы хотя бы старые могли доработать

{% cut "Как этим пользоваться" %}

Сгенерировать sv-сервис для процесса (на ppcback'е)
```
# create-ptkill-for-operator <шард> <uid_оператора>
sudo create-ptkill-for-operator 9 610169176
```
Это создаст сервис с именем `ptkill.ppcdata9.operator=610169176`, которым можно управлять командой `sv` [документация](http://smarden.org/runit/sv.8.html)
```
yukaba@ppcback01e:~$ sudo sv status /etc/service/ptkill.ppcdata9.operator\=610169176
run: /etc/service/ptkill.ppcdata9.operator=610169176: (pid 536629) 31207s
yukaba@ppcback01e:~$ sudo sv stop /etc/service/ptkill.ppcdata9.operator\=610169176
ok: down: /etc/service/ptkill.ppcdata9.operator=610169176: 0s, normally up
yukaba@ppcback01e:~$ sudo sv start /etc/service/ptkill.ppcdata9.operator\=610169176
ok: run: /etc/service/ptkill.ppcdata9.operator=610169176: (pid 394445) 1s
```
За переключением мастера следит отдельный сервис `/etc/service/ptkill-for-operator.watcher`: прибивалка при запуске пишет в файл `master_host`, для какого мастера запустилась, watcher сравнивает с db-конфигом и перезапускает, если нужно. Логи в `/var/log/yandex/ptkill-for-operator.watcher.log`

Если надо вычистить сервис
```
sudo update-service --remove /etc/sv/ptkill.ppcdata9.operator\=610169176
sudo rm -rf /etc/sv/ptkill.ppcdata9.operator\=610169176
```
Как регулировать: в директории `/etc/service/ptkill.ppcdataN.operator=M` (которая является символической ссылкой на `/etc/sv/ptkill.ppcdataN.operator=M`) можно создать файлы, которые читаются при запуске.
```
# команды выполняются под root
cd /etc/service/ptkill.ppcdataN.operator=M
printf 10 > PT_KILL_LEAVE_ALIVE # сколько запросов от оператора оставить живыми
printf 20 > pt-kill_query-count # сколько запросов от оператора должно одновременно выполняться, чтобы стриггерить отстрел
printf 5 > pt-kill_interval # как часто (в секундах) проверять список запросов
# после изменения настроек надо перезапустить сервис
# префикс /etc/service необязателен
sv restart ptkill.ppcdataN.operator=M
```
Как передаются эти параметры и их значения по умолчанию можно посмотреть тут: https://a.yandex-team.ru/arcadia/direct/infra/direct-utils/mysql-ptkill2/ptkill.template_for_operator.sv

{% endcut %}


