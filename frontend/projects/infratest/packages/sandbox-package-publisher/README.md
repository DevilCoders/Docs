# Sandbox package publisher

Утилита собирает пакет со всеми необходимыми `node_modules` и публикует в sandbox.

Есть возможность добавить в архив node executable файл (для платформы, на которой была запущена команда), указав флаг --addNode (-a). В этом случае в атрибуты sandbox ресурса будет **автоматически добавлена нужная платформа**.

С помощью опции --resourceAttributes (-r) можно передать необходимые атрибуты в создаваемый sandbox ресурс. Например так: `-r ttl=inf backup_task=true`. **Важно** - `yargs` воспринимает команду `upload`, идущую в конце, как часть массива `resourceAttributes`, поэтому не стоит писать так `-r ttl=inf upload`.

## Использование

Для использования необходима утилита [ya](https://wiki.yandex-team.ru/yatool/distrib/)
```shell script
sandbox-package-publisher upload --name=NAME --type=TYPE [--addNode] [--resourceAttributes name1=value1 name2=value2]
```
