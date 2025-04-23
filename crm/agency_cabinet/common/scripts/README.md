# Подготовка окружения для PyCharm (актуальный способ)
0. Запускаем в корне проекта команду
    > ya ide pycharm
1. Теперь у нас есть подготовленные бинари для всех тестов и модулей

# Подготовка окружения для PyCharm (старый способ)

0. Определяем переменную с путем до корня Аркадии: $ARCADIA_PATH
1. Запускаем сборку, которая сгенерирует определения протобаффов (для подсветки в IDE)
   и аркадийный бинарь
   - >cd $ARCADIA_PATH/crm/agency_cabinet && ya make --add-protobuf-result
2. Берем аркадийный бинарь и делаем его интерпретатором проекта:
   - Preferences | Project: <project_name> | Python Interpreter
   - ⚙ | Add | System Interpreter
   - Указываем путь:
      - > $ARCADIA_PATH/crm/agency_cabinet/common/scripts/bin/python
3. Если какие-то импорты не подсвечиваются даже с [аркадийныйм плагином](https://a.yandex-team.ru/arc/trunk/arcadia/devtools/intellij), то
  в настройках интерпретатора добавляем пути:
   - Preferences | Project: <project_name> | Python Interpreter | ⚙ | Show all |
   - Выбираем аркадийный интерпретатор
   - Жмем на символ ![](https://jing.yandex-team.ru/files/danielbord/image.svg)
   - Добавляем пути к аркадийным библиотекам, например (библиотеки с которыми
  у меня были проблемы):
     - > $ARCADIA_PATH/library/python/yenv
     - > $ARCADIA_PATH/arcadia/contrib/python/alembic
     - > $ARCADIA_PATH/contrib/python/sqlalchemy/sqlalchemy-1.2
     - > $ARCADIA_PATH/contrib/python/celery
     - > $ARCADIA_PATH/contrib/python/asgiref/py3
     - > $ARCADIA_PATH/arcadia/yt/python/yt
     - > $ARCADIA_PATH/contrib/python/marshmallow/py3
   - Добавляем аркадийный путь к стандартным библиотекам Python
     - > $ARCADIA_PATH/contrib/tools/python3/src/Lib
   - С плагином и этим интерпретатором должно работать большинство импортов, а так же
  можно запускать тесты из Pycharm
   - В качестве рабочей директории лучше указывать корень Аркадии, т.к. некоторые костыли
  для запуска тестов локально могут на это опираться
4. Запускать скрипты/тесты под этим интерпретатором удобно, если определена переменная
$Y_PYTHON_SOURCE_ROOT
(**N.B**: не стоит определять ее глобально, например, в ~/.bashrc, т.к. это
   может сломать ya tools и другие инструменты)

# TODO: добавить еще всякой полезной инфы
