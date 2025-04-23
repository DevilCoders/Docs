# train_admin
Админка для поездов

### Локальный запуск
Сборка: `ya make`

Запуск: `manage/manage runserver` (запуск с помощью Django) или `wsgi/wsgi` (запуск gunicorn)

### Локальный запуск в docker образе
1. В package.json поменять версию на unstable
2. Отредактировать dev_env.list, в частности, прописать настройки вашей postgress базы
3. Собрать docker образ `ya package package.json --docker`
4. Запустить `docker run --network=host --env-file ./dev_env.list registry.yandex.net/rasp/train-admin:unstable`
5. После внесения изменений нужно повторить пункты 3 и 4

### Сборка и деплой docker образа
Изменяем версию пакета в `package.json`. Далее запускаем (не обязательно в корне проекта):
```shell script
mkdir -p rasp
ya package package.json --docker
docker push registry.yandex.net/rasp/train-admin
```

### Применение и добавление ролей
Чтобы пользователю можно было зайти в сервис, ему необходима роль. Роли можно запросить в idm:
[тест](https://idm.yandex-team.ru/system/train-admin-test/roles#rf=1,rf-role=1#train-admin-test),
[прод](https://idm.yandex-team.ru/system/train-admin/roles#rf=1,rf-role=1#train-admin)

Новые роли появляются при добавлении новой группы в таблицу `auth/group`.
Чтобы после этого роль появилась в idm, владельцу нужно синхронизировать узлы.

### Применение миграций
Локально: `manage/manage migrate`

На сервере: `DJANGO_SETTINGS_MODULE=travel.rasp.trains.train_admin.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.trains.train_admin.manage.manage:main /app/app migrate`

### Загрузка фикстур
Фикстуры это json формат хранения данных в Django. С их помощью можно заполнить базу данных.
Фикстуры хранятся в `train_admin/fixtures`.

Чтобы загрузить фикстуру локально: `manage/manage loaddata имя_фикстуры.json`

Загрузить все фикстуры локально: `./manage/manage loaddata ./train_admin/fixtures/*.json`

Чтобы загрузить фикстуру на сервере: `DJANGO_SETTINGS_MODULE=travel.rasp.trains.train_admin.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.trains.train_admin.manage.manage:main /app/app loaddata имя_фикстуры.json`

### Запуск shell и dbshell
С помощью команды `shell` можно запустить консоль приложения.
С помощью `dbshell` можно запустить консоль базы данных: параметры подключения не нужно указывать, они автоматически возьмутся из настроек.
**Для dbshell должен быть установлен psql.**

Локально: `manage/manage shell` или `manage/manage dbshell`

На сервере: `DJANGO_SETTINGS_MODULE=travel.rasp.trains.train_admin.docker.local_settings Y_PYTHON_ENTRY_POINT=travel.rasp.trains.train_admin.manage.manage:main /app/app shell`
