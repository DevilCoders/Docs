Проект:
------------
То, чего вы всегда хотели, но боялись спросить: перекладываем json'ы настраивая excel!

Запуск тестов:
------------
```
ya make -j6 -ttt .
```

Генерация миграции:
------------
Из корня проекта собираем основной бинарик и запускаем его, пробрасывая как точку запуска manage.py, файл настроек, окружение для sqlite:
```
ya make -j6 src/wsgi/ && Y_PYTHON_ENTRY_POINT="intranet.table_flow.src.manage" DJANGO_SETTINGS_MODULE=intranet.table_flow.src.settings YENV_TYPE=development.migration ./src/wsgi/table_flow.wsgi makemigrations
```

Накатка миграции
------------
```
cat /proc/`pgrep table_flow | head -1`/environ | tr "\0" "\n" > .env
vim .env
```

Далее в файле обрамляем в двойные кавычки пароль от базы
```
source .env && export $(cut -d= -f1 .env)
MIGRATE=1 table_flow migrate
```

IDM
------------
Тестовая система: table_flow_testing
Система для прода: table_flow

Как заставить работать env при подключении по ssh в деплой:
------------
```
cat /proc/`pgrep table_flow | head -1`/environ | tr "\0" "\n" > .env && source .env && export $(cut -d= -f1 .env)
```
