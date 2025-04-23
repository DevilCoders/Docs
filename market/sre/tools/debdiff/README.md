## debdiff

debdiff - compare installed package files with files from debian package

this tool has been written for task [st/CSADMIN-14074](https://st.yandex-team.ru/CSADMIN-14074) and [tsum-agent](https://github.yandex-team.ru/market-infra/tsum/tree/master/tsum-agent)


### Usage:

```
debdiff-bin FILES
```

FILES - files in package to check

### Examples:

1. compare file /etc/bash.bashrc on the file system with original file in debian package

```
debdiff-bin bash /etc/bash.bashrc
Get:1 http://mirror.yandex.ru/ubuntu/ trusty-updates/main bash amd64 4.3-7ubuntu1.5 [576 kB]
Fetched 576 kB in 0s (8,309 kB/s)
--- /tmp/debdiff/tmpzYcr7i/bash-4.3-7ubuntu1.5/pkg/etc/bash.bashrc
+++ /etc/bash.bashrc
@@ -30,11 +30,11 @@

 # enable bash completion in interactive shells
 #if ! shopt -oq posix; then
-#  if [ -f /usr/share/bash-completion/bash_completion ]; then
-#    . /usr/share/bash-completion/bash_completion
-#  elif [ -f /etc/bash_completion ]; then
-#    . /etc/bash_completion
-#  fi
+  if [ -f /usr/share/bash-completion/bash_completion ]; then
+    . /usr/share/bash-completion/bash_completion
+  elif [ -f /etc/bash_completion ]; then
+    . /etc/bash_completion
+  fi
 #fi

 # sudo hint
```


### links

[sandbox job to build debian package](https://sandbox.yandex-team.ru/task/91691005/view)