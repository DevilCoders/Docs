# Использовать executer для выполнения команд сразу на многих машинах (виртуалках)

## Теория { #theory }

Executer -- Яндексовая разработка; программа для запуска команд сразу на многих серверах (виртуалках). Чуть больше теории: [{#T}](../things/executer.md)

## Примеры полезных команд { #examples }

### Режим команды с параметрами

Этот режим хорош для встраивания executer в конвейеры.

```
# прорефрешить кеш Няни
executer exec 'n:production_market_mbi_billing*' hostname -f

# -c велит использовать кеш Няни; работает быстрее
executer -c exec 'n:production_market_mbi_billing*' 'ps -Ao pid,start,user,fname,tmout,f,comm,wchan |grep java'

# с -q меньше украшений в выводе
executer -c -q exec 'n:production_market_mbi_billing*' 'ps -Ao pid,start,user,fname,tmout,f,comm,wchan |grep java'

# p_exec -- запустить команды на всех серверха параллельно
executer -c -q p_exec 'n:production_market_mbi_billing*' 'ps -Ao pid,start,user,fname,tmout,f,comm,wchan |grep java'
```

### Режим шелла

Этот режим хорош для интерактивного выполнения чего-нибудь.

Запускаем `executer` или `executer -c`. Дожидаемся приглашения в духе `[Serial] <login>>`.

Даем команды, начиная с `exec` или `p_exec`:

```
exec n:production_market_mbi_billing* ps -Ao pid,start,user,fname,tmout,f,comm,wchan |grep java
```


## Настройки, удобные для Биллинга Маркета { #settings }

В файл `~/.executer.conf` записать:

```
default_user = <вписать свой логин>
# раньше тут была настройка "sudo = 1", но
# 1) этот конфиг не у всех везде может быть, и тогда лучше в инструкциях явно указывать команды с sudo (по умолчанию в executer sudo = 0)
# 2) с sudo = 1 введённая команда вида "cmd1; cmd2" выполнится как "sudo cmd1; cmd2", что может привести к неожиданностям
sudo = 0
rtc_disabled = 0
qloud_disabled = 1

rtc_cache_file = ~/.executer/.rtc_cache

rtc_token = <https://nanny.yandex-team.ru/ui/#/oauth/ -- по этой ссылке взять токен и вписать сюда, без угловых скобок>

nanny_filter = market/market_billing/
nanny_filter = market/mbi/
```

* Поправить два места: свой логин и oauth-токен
* `mkdir -p ~/.executer/.rtc_cache`


## Установка { #install }

Executer можно установить на Mac, Linux. Возможно, на Windows тоже, поверх cygwin (непроверенная инфа).

Инструкции см. в официальной доке: <https://wiki.yandex-team.ru/executer>

Критерий успеха: команды

```
executer exec 'n:production_market_market_billing_tms_*' hostname -f

executer exec 'n:production_market_market_billing_tms_*' uptime
```

(локально) запускаются и показывают результат выполнения на 6 машинках



## Ссылки { #links }

* Документация executer: <https://wiki.yandex-team.ru/executer>

