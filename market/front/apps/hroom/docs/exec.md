# exec

В src/bin/exec.ts находятся таски, которые запускают модельные методы.
Для запуска тасков из консоли необходимо воспользоваться командой:
```bash
npm run exec -- <comman_name>
```

У тасков есть несколько вариантов применения:
 - разработка. По сути, возможность запускать из консоли таски командой является альтернативой работы через TDD.
Можно написать таск, который будет дергать какие-то модельные методы, что-то запускать, ...
 - запуск команд. Можно описать логику вызова модельных методов, добавить описание о том, что делать данный таск, а потом добавить команду для его вызова в ```npm run <command>```.
Или не добавлять, а вызывать напрямую через ```npm run exec <task> -- <params>```