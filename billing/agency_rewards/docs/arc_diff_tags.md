Различия между версиями
=======================

Т.к. мы уже больше не в git'e, надо учиться делать "это" самим.
Arc, RM ничего такого (пока) не предоставляют.


Скачиваем версии
-----------------

Например, мы хотим сравнить 14.6 и 15.1:

```bash
$ cd /tmp
$ svn co svn+ssh://arcadia.yandex.ru/arc/tags/agency_rewards/14.6/arcadia/billing/agency_rewards 14.6
$ svn co svn+ssh://arcadia.yandex.ru/arc/tags/agency_rewards/15.1/arcadia/billing/agency_rewards 15.1
```

Различающиеся файлы
-------------------

```bash
$ diff -rq 14.6 15.1 | grep -v ".svn" | head                         
Files 14.6/agency_rewards/calculate.py and 15.1/agency_rewards/calculate.py differ
Files 14.6/agency_rewards/client_testing.py and 15.1/agency_rewards/client_testing.py differ
Files 14.6/agency_rewards/common/__init__.py and 15.1/agency_rewards/common/__init__.py differ
Files 14.6/agency_rewards/config.py and 15.1/agency_rewards/config.py differ
Files 14.6/agency_rewards/m/base.py and 15.1/agency_rewards/m/base.py differ
Files 14.6/agency_rewards/m/market.py and 15.1/agency_rewards/m/market.py differ
Files 14.6/agency_rewards/m/prof.py and 15.1/agency_rewards/m/prof.py differ
Files 14.6/agency_rewards/main/main.py and 15.1/agency_rewards/main/main.py differ
Files 14.6/agency_rewards/scheme.py and 15.1/agency_rewards/scheme.py differ
Files 14.6/agency_rewards/utils/argument_parsers.py and 15.1/agency_rewards/utils/argument_parsers.py differ
```

Это, конечно, не `git diff --stats ...`, но лучше, чем ничего.

Полная разница
--------------

```bash
$ diff -r 14.6 15.1 | colordiff | less -R
```
