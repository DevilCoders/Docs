# Как синкать файлы на виртуалку через realsync

*шаги 3-5 только для macOS Catalina и выше, описание тут - https://github.com/DmitryKoterov/dklab_realsync/issues/43

1. Идем в https://github.com/DmitryKoterov/dklab_realsync
2. Клонируем репозиторий `git clone git@github.com:DmitryKoterov/dklab_realsync.git`
3. Идем в сорс файлы`cd dklab_realsync/src/darwin`
4. Компилим файл notify `cc -framework CoreFoundation -framework CoreServices -o notify notify.c`
5. Переносим его в аналогичную директорию в bin `cp notify *path-to-dklab_realsync-folder*/bin/darwin/`
6. Идем в папку с realsync `cd *path-to-dklab_realsync-folder*`
7. Запускаем синк (в первый раз будет интерактивный визард) `perl realsync *path-to-your-sync-folder*`
8. Проходим все шаги интерактивного визарда, останавливаемся перед "Press enter to start sync"
9. Идем в директорию, которую собрались синкать, ищем там файл .realsync, находим там строчку `exclude_file = .gitignore` и раскоменчиваем ее. Так ничего лишнего не будет синкаться.
10. Работаем. Чтобы все синкалось, нужно держать команду из пункта 7 в консоли запущенной.
