# YaIncBot

1. Идём в сервис [YaIncBot](https://nanny.yandex-team.ru/ui/#/services/catalog/searchmon_bot_docker/)
2. В блоке **Runtime** открываем вкладку **Instance Spec**
3. В контейнере **bot** разворачиваем спойлер **Environment variables configuration**
4. Меняем значение переменной **ZERO_DIFF** на любое другое число
5. В блоке **Runtime** нажимаем **Save**
6. В появившемся окне в разделе **Comment** пишем **"zerodiff"**, нажимаем **Submit**, у сервиса появляется новый снапшот.
7. В новом снапшоте **Change -> Active**


{% cut "То же самое, но в картинках" %}

1. Идём в сервис **YaIncBot**, во вкладку [InstanceSpec](https://nanny.yandex-team.ru/ui/#/services/catalog/searchmon_bot_docker/instance_spec)

    ![Вкладка Instance Spec ](_screenshots/runtime_instance_spec.png "InstanceSpec" =800x600)

2. В контейнере **bot** разворачиваем спойлер **Environment variables configuration** и меняем значение переменной **ZERO_DIFF** на любое другое число

    ![Environment variables configuration ](_screenshots/bot_env_var_conf.png "Environment variables configuration" =800x600)

3. Сохраняем значение, в комментарии к новой конфигурации пишем "zerodiff", у сервиса появляется новый снапшот.

    ![ Save ](_screenshots/runtime_save.png "Runtime Save" =800x600)

4. Активируем новый снапшот

    ![Active](_screenshots/active.png "Active" =800x600)

{% endcut %}
