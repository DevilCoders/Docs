# How-to: обновление Skotty

Skotty, как и любая иная приложенька, не может обойтись без новых фичей и валенков, поэтому его нужно периодически обновлять.

### Как проверить версию
```
$ skotty version
Version: 0.9.8476990
Build at: 2021-08-02 03:09:53 +0300 MSK
Arc info:
    Branch: 6d1a21f6653358781ebec74f121de34b76e4f943
    Commit: 6d1a21f6653358781ebec74f121de34b76e4f943
    Author: buglloc
    Summary: SKOTTY-4 added periodic certs lifetime/skotty version check

Other info:
    Build by: sandbox
    Top src dir: /place/sandbox-data/tasks/9/4/1034869249/__FUSE/mount_path_6af64c08-0bab-44f7-a4d9-8d341ac204f5
    Top build dir: /place/sandbox-data/build_cache/yb
    Hostname: linux-ubuntu-12-04-precise
    Host information: 
        Linux linux-ubuntu-12-04-precise 4.19.183-42.2mofed #1 SMP Wed Apr 21 14:40:19 UTC 2021 x86_64
```

В случае, если новая версия есть - skotty подскажем вам это:
```
$ skotty                
-----
New Skotty version available (cur v0.9.8473154): v0.9.8476990
-----
[...]
```

Так же, если запущен агент - он сам периодически проверяет версию и выводит вам нотификашку, в случае обнаружения новой версии.

### Как же обновиться

Если вы не помните, используете вы лончер или нет - это можно легко проверить, с помощью флага `--is-launcher`:
```
# это лончер
$ skotty --is-launcher
yep

$ echo $?
0

# а это нет
$ skotty --is-launcher  
nope

$ echo $?
1
```

{% list tabs %}

  - Для пользователей лончера

    Можно как проверить наличие новой версии:
    ```
    $ skotty --has-update 
    No updates availabe. You are using the latest version.

    $ skotty --has-update                   
    New version available: 0.9.8476990
    ```

    Так и обновиться:
    ```
    $ skotty --update             
    2021-08-03T10:54:35.293+0300    info    request latest version
    2021-08-03T10:54:35.369+0300    info    latest version is: 0.9.8476990
    2021-08-03T10:54:35.369+0300    info    prepare release dir
    2021-08-03T10:54:35.370+0300    info    downloading...
    2021-08-03T10:54:35.833+0300    info    release downloaded into: /home/buglloc/.skotty/releases/0.9.8476990/skotty
    2021-08-03T10:54:35.894+0300    info    clean up old release
    2021-08-03T10:54:35.895+0300    info    removed old release: 0.9.8473154
    2021-08-03T10:54:35.895+0300    info    skip release: 0.9.8476990
    2021-08-03T10:54:35.895+0300    info    updating current release info
    Updated to version: 0.9.8476990
    ```

  - Для всех остальных

    Откуда ставили, там и обновляйте.

{% endlist %}