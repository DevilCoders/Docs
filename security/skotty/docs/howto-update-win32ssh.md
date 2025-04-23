# Обновление Win32OpenSSH

К ложалению, OpenSSH в Windows довольно староват и должен быть обновлен в обновлении 22H1, но похоже этого так и не случилось.
Поэтому наиболее простой способ заполучить себе свеженький Win32OpenSSH - установить его из [оффициальной репы](https://github.com/PowerShell/Win32-OpenSSH).

Если говорить точнее, то необходимо:
  1. Установить свежую версию Win32OpenSSH Win64 из [оффициальной репо](https://github.com/PowerShell/Win32-OpenSSH)
  2. Остановить службу `ssh-agent` (она конфликтует со Skotty)
  3. Поправить __системные__ переменные окружения, добавив туда путь `C:\Program Files\OpenSSH` перед `%SYSTEMROOT%\System32\OpenSSH\`

Вы можете сделать это вручную или воспользоваться специальным установщиком, который сделает это все за вас. Для этого:
  - Открываем PowerShell консоль от имени Администратора
  - Выполняем в ней:
```
Invoke-WebRequest -Uri "https://tools.sec.yandex-team.ru/api/v2/dumb-proxy/win32ssh-installer/8.9.1-1/win32ssh-installer-windows-amd64.zst/win32ssh-installer-windows-amd64/win32ssh-installer_windows_amd64_8.9.1-1.exe" -OutFile "$env:TEMP\win23ssh-installer.exe"
& "$env:TEMP\\win23ssh-installer.exe" install
Remove-Item -Path "$env:TEMP\win23ssh-installer.exe"
```
  - Перезапускаем терминал, чтоб новые переменные окружения точно применились
  - Проверем вызвав `ssh -V` :)

Если в результате работы установщик жалуется на то, что OpenSSH уже установлен - удалите его в соответствующем разделе панели управления.
На всякий случай, демо:
  - Windows 11:
  ![start powershell](_assets/start-powershell-win11.png)
  ![w32ssh installer](_assets/w32ssh-installer-win11.png)
  - Windows 10:
  ![start powershell](_assets/start-powershell-win10.png)
  ![w32ssh installer](_assets/w32ssh-installer-win10.png)
