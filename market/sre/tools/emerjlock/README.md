# Стопкран emerjlock

Используется на *slb-серверах для проведения безопасных ручных работ, чтобы никакая автоматика в это время ничего не выкатила и не перепнула.

[emerjlock](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/tools/emerjlock) - это утилита для ручного взведения стопкрана и для ручной или автоматической проверки того, не взведен ли кем-то стопкран.
По замыслу выставлять и снимать стопкран можно только вручную. Проверять же его должна вся автоматика на сервере, чтобы не навредить.

Все действия утилиты emerjlock логгируются (по уммолчанию в **/var/log/emerjlock**).

```shell
# Взвести стопкран
emerjlock set

# Снять стопкран
emerjlock unset

# Проверить, взведен ли кем-то стопкран
emerjlock check
Emerjlock is set. e-a-sokolov set this lock at 2021.05.31 04:45:05 (+0300 GMT) by command 'emerjlock set'

# Проверка в скриптах может производиться в тихом режиме. Код ответа 0 - стопкран не установлен, 1 - установлен.
emerjlock -q check

# Выполнить заданную команду, если стопкран не взведен
emerjlock -- echo aaa
aaa

emerjlock set
emerjlock -- echo aaa
Emerjlock is set. e-a-sokolov set this lock at 2021.05.31 04:45:05 (+0300 GMT) by command 'emerjlock set'
```

