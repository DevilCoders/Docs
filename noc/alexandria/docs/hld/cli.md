## Alexandria CLI-binary
Пакет или бинарный файл александрии можно использовать в режиме CLI
Для этого необходимо правильно настроить TVM.

Реализовано:
* проверка настроек
* проверка версии и коммита
* вызов репорта

Работает help:
```
~/arcadia/noc/alexandria/cmd/alexandria$ ./alexandria report --help 
init app-clients, save single or multiple reps, exit 

Usage: 
 alexandria report [flags]

Flags: 
 -h, --help               help for report 
 -m, --multiple strings   Tuple of pathes to the ='matchers.txt,softs.yaml,objects.yaml' 
 -r, --rackcode string    Filter RT objects by RackCode (default "not {$nameless}") 
 -s, --single string      Path to the file with output 

Global Flags: 
 -c, --config string   Path to the config file


```

Для доступа запросов, провоцирующих общение с INVAPI, может [понадобиться TVM](../dev/components/tvm)
Репорты пока вызывают только робот nocdev-ci и команда разработки.