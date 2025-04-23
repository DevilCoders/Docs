# Role Migrator
Generate liquibase migration files for wms infor roles

##Использование
Для начала необходимо убедиться что нужная роль есть у всех пользователей преста с префиксом user_login. Для автотестов AT.
```console
brew install unixodbc
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql mssql-tools

python3 setup.py install
ln -s /usr/local/opt/python@3.9/Frameworks/Python.framework/Versions/3.9/bin/role-migrator /usr/local/bin/role-migrator
```
Перед запуском скрипта, необходимо добавить настройки для подключения к бд преста в файл ~/.migrator.properties. Взять в секретнице пользователя DbWmsAdminUser.

```
server=<hostname>
port=<port>
username=<database username>
password=<database password>
```
Далее переходим в папку /arcadia/market/logistics/wms/utils/role-migrator и запускаем:
```
role_migrator -a <author> -t <startrack task id> -r <role name> -d <filename description> -o <output dir> -u <user_login> --user-range <login_number_max_range>
```
##Пример:
```
role-migrator -a ankuant -t MARKETWMS-13615 -r 'Сортировка BBXD' -d add-bbxd-sorting-role -u AT --user-range 200
```

В результате мы получим файлы:
* utils/role-migrator/out/SCPRDD1/migrations/2022-06-29-MARKETWMS-13615-add-bbxd-sorting-role.sql
* utils/role-migrator/out/SCPRDD1/migrations/2022-06-29-MARKETWMS-13615-add-to-users.sql
* utils/role-migrator/out/SCPRDMSTM1/migrations/2022-06-29-MARKETWMS-13615-add-bbxd-sorting-role.sql

# Options

### author
Инициалы автора: afomichev

### Startrack task id
Номер задачи в startrack: MARKETWMS-1123

### Role name
Название роли для которой создаем миграцию: YM-YDM

### Filename description
Пояснение в названии файла миграции: ym-ydm-role

### Output dir
Директория в которую сохраняется новый файл с миграцией, по умолчанию 'out'. Можно не указывать при запуске

###User login
Префикс логина. В случае автотестов это AT

###Login number max range
Для всех логинов AT[1...login_number_max_range] будет добавлена роль.
В случае мультитестингов указываем 200.

#Название директории
Есть две базы данных в которые будут добавляться новые данные: SCPRDD1, SCPRDMSTM1
Файлы с миграцией помещаются по следующему пути
* output_dir/SCPRDD1/migrations/migration.sql
* output_dir/SCPRMSTM1/migrations/migration.sql

Например:

infor-sce/db-migrations/db/SCPRDD1/migrations/2021-04-26-MARKETWMS-1123-ym-ydm-role.sql

После того как получены миграции, необходимо переместить их в соответствующие папки app/db-migrations/liquibase/db и не забыть добавить в changelog-master.xml каждой из баз

#Название файла с миграцией
Название файла формируется так: today-taskid-desc.sql

* today дата в формате YYYY-MM-DD
* taskid номер задачи: MARKETWMS-1123
* desc описание миграции: ym-ydm-role

Например: 2021-04-26-MARKETWMS-1123-ym-ydm-role.sql
