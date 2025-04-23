Tableau backup script
===========================

Как собрать в .exe:

`
go get github.com/konsorten/go-windows-terminal-sequences
`

`
bash build.sh
`

Деплой. 

Так как это windows, автоматического деплоя не предусмотерено. Если нужно чтото изменить: 
* Собираем бинарь. 
* Складываем в диреткорию C:\ProgramData\Tableau\Tableau Server\data\tabsvc\files\backups

Чтобы работали бекапы и можно было собирать логи нельзя запускать напрямую exe-файл. 
Из Task Scheduler лучше запускать прослойку в виде powershell-скрипта backup.ps1. 
Запуск делается командой 
`
PowerShell -File "C:\ProgramData\Tableau\Tableau Server\data\tabsvc\files\backups\backup.ps1"
`
От имени пользователя-админа tableau. 
Тогда лог бекапа будет в файле backup.log. 
