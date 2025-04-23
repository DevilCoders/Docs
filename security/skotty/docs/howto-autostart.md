# How-to: автозагрузка

{% list tabs %}

  - GNU/Linux
  
    Skotty можно установить в качестве пользовательского systemd-юнита, о чем он спрашивает в процессе первичной настройки.
    Если вы передумали, его всегда можно заново включить или отключить с помощью `skotty service enable/disable`.
    В остальном это обычный systemd-юнит, поэтому `systemctl` ваш лучший друг ;)

  - macOS
  
    Skotty можно установить в качестве сервиса (launch agent), о чем он спрашивает в процессе первичной настройки.
    Если вы передумали, его всегда можно заново включить или отключить с помощью `skotty service enable/disable`.
    В остальном это обычная launchd джоба, поэтому `launchctl` ваш лучший друг:
    ```
    % ps aux | grep skotty
    buglloc           5849   0.0  0.0 408103312   1344 s001  S+   10:45AM   0:00.00 grep --color=auto skotty
    buglloc           5836   0.0  0.4  9082412  63408   ??  S    10:45AM   0:00.11 /Users/buglloc/.skotty/releases/0.9.8474332/skotty start
    buglloc           5833   0.0  0.2  9074140  36624   ??  S    10:45AM   0:00.05 /usr/local/bin/skotty start

    % launchctl list | grep skotty
    5833 0 ru.yandex.skotty

    % launchctl stop ru.yandex.skotty

    % ps aux | grep skotty
    buglloc           5860   0.0  0.0 408112528   1408 s001  S+   10:46AM   0:00.00 grep --color=auto skotty

    % launchctl start ru.yandex.skotty

    % ps aux | grep skotty
    buglloc           5870   0.0  0.0 408103312   1344 s001  S+   10:46AM   0:00.00 grep --color=auto skotty
    buglloc           5867   0.0  0.4  9083692  63328   ??  S    10:46AM   0:00.11 /Users/buglloc/.skotty/releases/0.9.8474332/skotty start
    buglloc           5864   0.0  0.2  9076184  36528   ??  S    10:46AM   0:00.05 /usr/local/bin/skotty start
    ```

  - Windows
    
    Под Windows дела не так радужны и Skotty может лишь добавить себя в автозагрузку дедовским способом (i.e. в ветку реестра `HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`). Он спрашивает об этом в процессе первичной настройки, но вам никто не мешает в любой момент передумать и добавить/убрать его оттуда: `skotty service enable/disable`.

{% endlist %}