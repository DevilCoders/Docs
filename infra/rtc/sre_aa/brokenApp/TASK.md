# Задача brokenApp

## При запуске программа падает c "fatal error: runtime: out of memory", нужно ответит почему так, на каком системном вызове

Что хотим увидеть:  
запустить strace и найти падающий mmap:  
`mmap(0xc004000000, 8796093022208, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = -1 ENOMEM (Cannot allocate memory)`

## Дальше просим попробовать починить

Что хотим увидеть:  
Тут нужно заметить сообщения при старте и понять, что дело в размере BufferSize    
`Starting new instance...`   
`Config: BufferSize = 1099511627776`   
`Config: Threads = 200`   
`Config: Data sources = [localhost:80 localhost:81]`  
`fatal error: runtime: out of memory` 

Нужно понять откуда оно берется, в strace найти open*   
`openat(AT_FDCWD, "/usr/local/var/run/.broken_app.default.huge_instance.conf", O_RDONLY|O_CLOEXEC) = 3`

Отредактировать конфиг на более внятные параметры   
+1 если заметить что перед этим brokenApp пробует найти конфиг в $HOME/.broken_app.conf, потому лучше не редактировать стандартный конфиг, а сделать свой

## После запуска в консоль станет падать что-то типа
Found long request_id 0 (1152.0 ms), see logs for details   
Нужно найти куда пишется лог

Что хотим увидеть:   
lsof   
\+ /proc/X/fd

## Понять какие запросы тормозят

Что хотим увидеть:  
В логе нужно найти по времени и номеру запроса какие запросы тормозят   
окажется что тормозят запросы одного треда к одному data source

## Понять почему запросы тормозят

Что хотим увидеть:  
Хотим увидеть приличное число ретрансмитов сравнительно с другими запросами 

`Напоминалка:`   
`Есть хосты с nginx, один из них активно дропает пакеты и должен выделяться в tcpdump числом ретрансмитов`
