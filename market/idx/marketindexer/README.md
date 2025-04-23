# mindexer_clt
Точка входа во все части/программы индексатора.

Примеры команд:
```
mindexer_clt show
mindexer_clt master_info
```

Получить права corba:
```
manushkin@mi01v:~$ sudo mindexer_clt run_corba_shell
corba@mi01v:/home/manushkin$
```

Получить права root:
```
manushkin@mi01v:~$ sudo mindexer_clt run_root_shell
root@mi01v:/home/manushkin#
```

# massindexer
Демон большого индексатора.
Собирает поколения в бесконечном цикле, используя `mindexer_clt build_mass_index`.
