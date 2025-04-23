## Диагностика офферов - Doctor

### Локальный запуск

1. Создать проект IDEA через `bin/create-idea-project-with-libs.sh`
2. В аргументах VM добавить:
    ```
   -Dconfigs.path=${ARCADIA_ROOT}/market/mbo/doctor/src/main/properties.d
    ```
3. В environment variables должны быть:
    ```
    ETCD_USERNAME=datasources_read_all;ETCD_PASSWORD=<password>
    ```

### Работа с TVM
   1. Если не нужно проверять запросы к blackbox, то можно добавить в environment variables
      ```
      LOCAL_DEV_USER_LOGIN=your_login
      ```
   2. А если нужно запустить приложение локально со всеми запросами к blackbox и TVM нужно
      1. Установить tvm-tool
         ```
         sudo pip3 install tvmtool-bin -i https://pypi.yandex-team.ru/simple
         ```
      2. Сгенерировать случайную строку из 32 символов в качестве локального токена (например sabfhsdbfjsjnjsnfj45t4wn23urb432)
         ```
         openssl rand -hex 16 > ~/.tvmtool-token
         ```
      3. Сгенерировать конфигурацию tvm. Вместо <СЕКРЕТ> подставить значение, выданное для TVM доктора и хранящееся в секрете. Узнать можно в ABC doctor
         ```
         tvmtool add --secret "<СЕКРЕТ>" --src 2033833:doctor --dst 225:blackbox
         ```
      4. Запускаем tvmtool, важно sudo ставить в самое начало, чтобы tvmtool увидел переменную окружения. В данном случае tvmtool находится по адресу localhost:2
         ```
         sudo TVMTOOL_LOCAL_AUTHTOKEN=`cat ~/.tvmtool-token` tvmtool --port 2
         ```
      5. Добавляем переменные окружения (environment variables)
         
         | var | value | description |
         | --- | --- | --- | 
         | DEPLOY_TVM_TOOL_URL | http://localhost:2 | Адрес, где разворачивается tvmtool |
         | TVMTOOL_LOCAL_AUTHTOKEN | sabfhsdbfjsjnjsnfj45t4wn23urb432 | сгенерированная строка из пункта 2 |
         | LOCAL_DEV_HOSTNAME | https://doctor.market.yandex-team.ru | Хост доктора, от которого присылаем запросы в blackbox |
         | LOCAL_DEV_CLIENT_IP |  | Свой IP адрес |
