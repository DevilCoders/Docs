Как тестировать загрузку словаря
================================

Коротко о главном
-----------------
Проверить выгрузку вашего нового словаря (одного или нескольких) можно с помощью теста [LoadDictionaryITest.testLoad()](java/ru/yandex/market/stat/dicts/loaders/LoadDictionaryITest.java).

Тест принимает на вход имена тестируемых словарей и выгружает 100 первых строк из тестовой базы на yt.

**Где смотреть результат?** <br>

   Результат можно посмотреть на кластере Hahn в вашей директории ```//tmp/<user_name>/<имя словаря>```

**Что потребуется для запуска?**:

- каркас аркадии + проект mstat/components локально

- yt токен

  Если вы раньше не работали с yt, то для начала вам потребуется получить токен и обзавестить личной директорией ```//tmp/<user_name>``` на клатере Hahn

- пароль от тестинга системы-источника

- дырка от вас до тестинга системы-источника (обычно есть по умолчанию. если нет - puncher в помощь)


Этапы запуска
--------------
1) Вычекнуть проект и собрать его
2) Прописать 2  проперти в local.properties
3) Вписать имя тестируемого словаря в тест и запустить из идеи

   или: вписать имя словаря в local.properties и запустить из консоли
4) Проверить, что выгрузилось в //tmp/<your_username> и формат столбцов вам нравится
5) Не коммитить изменения 2 и 3!


Сборка проекта
--------------
Нужно вычекнуть проект [mstat/components](https://a.yandex-team.ru/arc/trunk/arcadia/market/mstat/components)

[Документация про работу в аркадии](https://wiki.yandex-team.ru/market/projects/marketstat/dev/arcadia/#sborkaproekta)

пример команд на примере svn:

1) Скачиваем каркас аркадии если еще не
    ```bash
    svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone
    ```
2) Вычекиваем и собираем проект
    ```bash
    ya make market/mstat/components --checkout
    ```

3) **[Для запуска из идеи]**:
   Генерируем проект для идеи, если запуск будет через неё (можно запускать из консоли)

    из директории components:
    ```bash
    ya ide idea --group-modules=tree --iml-in-project-root --ascetic -DJDK_VERSION=17 -lr ~/idea/components/ .

    ```
    Если идея не настроена (jdk и ya-плагин), то см инструкцию в [доке](https://wiki.yandex-team.ru/market/projects/marketstat/dev/arcadia/#importjava-proektavintellijidea)


Настройка пропертей
--------------

Для того, чтобы интеграционный тест запустился, нужно определить проперти:
1) В файле [integration-tests.properties](https://a.yandex-team.ru/arc/trunk/arcadia/market/mstat/components/dictionaries-yt/src/integration-test/resources/integration-tests.properties) обычно менять ничего не нужно.
    Но если вы добавили новый источник выгрузки (а не просто новую таблицу), нужно добавить пропертю с паролем

    пример:
    ```
    dictionaries.loaders.market_crm.jdbc.password=
    dictionaries.loaders.ocrm.jdbc.password=
    dictionaries.loaders.replenishment.jdbc.password=
    ```
    В файле уже определены основные проперти, 99% из них могут быть пустыми. Тут главное, чтобы проперть фигурировала в файле.

2) Создать файл local.properties и не добавлять его в систему контроля версий (и не коммитить)
    ```
    тут: market/mstat/components/dictionaries-yt/src/integration-test/resources/local.properties
    ```

    В этом файле нужно добавить (переопределить) 2 проперти из integration-tests.properties:
    ```
    dictionaries.yt.token=<ваш личный токен в Yt>
    dictionaries.loaders.<ваш источник данных>.jdbc.password=<пароль для тестинга>
    ```
    **NB!!** Для удобства при запуске из консоли имя тестируемого словаря можно указать там же в _local.properties_
    ```
    dictionaries.to.test=my_super_dict
    ```
3) **[При запуске из идеи]**:

   Нажать ya->regenerate и build в  Idea (есть известный баг - после изменения пропертей идея перестает видеть проперти файл, ребилд это лечит)

   При запуске из консоли достаточно будет только поправить local.properties


Запуск теста
--------------
1) Передать имя словаря в тест. Можно сделать двумя способами:

    - непосредсвенно в коде теста [LoadDictionaryITest](java/ru/yandex/market/stat/dicts/loaders/LoadDictionaryITest.java)
    нужно переопределить переменную **DICT_FOR_TEST** - добавить туда имя тестируемого словаря.

    - прописать в local.properties параметр ```dictionaries.to.test```, а код теста оставить неизменным

    **NB!** Перед мержем в мастер нужно удостовериться, что параметр ```dictionaries.to.test```
    и переменная DICT_FOR_TEST пусты. Это проверяет тест testNoLoadsForCI.

    Как понять, что за имя у словаря - см ниже

2) Запустить тест:
    Можно сделать двумя способами:
    - через идею - запустить тест LoadDictionaryITest.testLoad()
      Плюсы: user-friendly, видно логи, можно менять тестируемый словарь на лету
      Минусы: нужно настраивать идею и собираеть проект
    - через консоль:
    ```bash
    cd market/mstat/components
    ya make -ttt -F ru.yandex.market.stat.dicts.loaders.LoadDictionaryITest::testLoad
    ```

Обычно тест отрабатывает за минуту (так как выкачивает только 100 строк из источника).


**Что такое имя словаря?**

В большинстве случаев имя словаря - значение из параметра destination в jdbc.config, без учета директории.
Если  destination не указан, он берется из имени таблицы на источнике.

Eсли словарь имеет кастомный скейл, имя словаря будет ```<dict_name>-<scale>```

**пример**
```
- source: some_db.aubergine
  destination: aubergine
  => aubergine

- source: some_db.carrot
  destination: mbo/carrot
  => carrot

- source: some_another_db.pumpkin
  => pumpkin

- source: some_db_again.sosiska
  destination: mbo/kolbaska
  scales:
    - scale: 1d
    - scale: 1h
  => kolbaska-1d
  => kolbaska-1h
```

Завершение тестирования
--------------
1) проверить глазами, что выгрузилось и формат данныхь на YT вас устраивает
   (обратить внимание на числовые поля/поля в формате json, иногда их необходимо поменять их тип)
2) выставить **DICT_FOR_TEST=""** вперед коммитом,
и убедиться что пароли  из  local.properties не попадут  в мастер


Как тестировать словарь из market-data-getter
------------------------------------------------

Либо просто копируем к себе из testing-окружения и временно меняем путь к getter.
Либо подмонтируем testing-директорию к себе используя sshfs

1) Установить последнюю версию https://osxfuse.github.io/
2) brew install sshfs
3) sudo mkdir -p /var/lib/yandex/market-data-getter
4) sudo chown $USER /var/lib/yandex/market-data-getter
5) sshfs mstgate01h.market.yandex.net:/var/lib/yandex/market-data-getter/  /var/lib/yandex/market-data-getter/
6) diskutil umount /var/lib/yandex/market-data-getter
7) diskutil umount force /var/lib/yandex/market-data-getter
