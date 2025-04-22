# Настройка локального стенда с применением Docker

*В качестве центральной утилиты управления стендом предполагается использование IDEА от JetBrains, т.к. в ней
представлены все необходимые плагины и для работы с репозиторием/ветками (Arcadia Plugin)
и для оркестрации образами/контейнерами Docker*

1. Если у тебя уже настроен стенд и ты переезжаешь в концепцию контейнеров, то не забудь отключить/удалить локальные
   nginx и postgresql, чтобы не было конфликта по портам

2. Если настройка впервые, то пройди стандартную [настройку](../../README.md), пропустив шаги установки node, yarn, nginx и
   postgresql

3. Чтобы работала аутентификация через yandex-team blackbox
    * Создай каталог `~/lilu-local/ssl`
      ```shell
      mkdir -p ~/lilu-local/ssl
      ```
    * Если ранее создавал ключи для ow.local.yandex-team.ru, то просто положи их в эту папку и переходи к следующему
      пункту
    * иначе, заказываем сертификат в [Сертификаторе](https://crt.yandex-team.ru/certificates)

      ![](docs/cert_request.png)

    * Сохраняем сертификат в каталог `~/lilu-local/ssl`
    * Создаем ключи
      ```shell
      cd ~/lilu-local/ssl
      openssl pkey -in ow.local.yandex-team.ru.pem -out ow.local.yandex-team.ru.key
      ```

4. Добавляем в `/etc/hosts` запись
   ```
   127.0.0.1 ow.local.yandex-team.ru ow.local.yandex.ru
   ```

5. Устанавливаем Docker согласно [инструкции](https://docs.docker.com/get-docker/)

6. Только для Linux
    * Ставим Docker Compose согласно [инструкции](https://docs.docker.com/compose/install/#install-compose)
    * Добавляем своего пользователя в группу docker
      по [инструкции](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user)

7. Настраиваем IDE
    * Убедись, что включен плагин Docker в настройках **Settings | Plugins**. Если его нет, поставь из Marketplace в том
      же окне настроек
    * В настройках IDE **Settings | Build, Execution, Deployment | Docker** добавь подключение к Docker кнопкой **+**.
      Все настройки оставь по умолчанию

8. В IDE в проекте находим каталог `operаtor-window` и открываем в нем файл `docker-compose.yml`

9. Установи свой пароль POSTGRES_PASSWORD согласно комментарию в `docker-compose.yml` (будет использоваться
   как пароль пользователя postgres локального стенда)

10. Поднимаем окружение, нажав `>>` в `docker-compose.yml` (рядом со строкой services)

11. Для запуска самого бека остается только запустить задачу `operator-window` настроенную на этапе
    стандартной [настройки](../../README.md)

*Как результат получаем полностью работающий локальный стенд, доступный в браузере по адресу ow.local.yandex-team.ru,
хранящий все свои файлы и базу в каталоге `~/lilu-local`*