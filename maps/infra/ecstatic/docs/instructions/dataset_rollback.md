# Откат датасета

1. Найти tvm id генераторов датасета в конфиге ecstatic.

    Это легко сделать с помощью codesearch в аркануме.  [Пример](https://a.yandex-team.ru/search?search=generate%20yandex-maps-jams-speeds,%5Emaps%2Fconfig%2Fecstatic%2Fstable%2F.*,jC,arcadia,,500&repo=arc_vcs)
    
    В примере мы находим все генераторы для датасета `yandex-maps-jams-speeds` в `stable` окружении ecstatic
2. Определиться, из какого бранча деплоится датасет на машинки. 
   
    Это видно в UI ecstatic в квадратных скобках перед названием деплой-группы. Например:
   ![Пример](../img/deploy_example.png)
   
   В этом примере датасет деплоится из `stable` бранча
3. В терминале надо подготовить все для работы с ecstatic tool

    ```shell
    export ENVIRONMENT_NAME = stable # или любое другое окружение
    export ECSTATIC_TVM_ID = 12345 # tvm id из пункта 1
    ```
   
4. Откатить версию из бранча:
    ```shell
    ecstatic move dataset:tag=version +branch_name/hold
    ```
   В примере `version` - откатываемая версия, `branch_name` - бранч из пункта 2

   Ecstatic выбирает для активации лексиграфически последнюю версию для активации в бранче. Т.е. для версий `a, b ,c` будет активирована версия `c`

   То есть, при откате версии `c` из бранча будет активирована версия `b`.