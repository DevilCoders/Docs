# Riverbank

###### Standalone [Yandex Stream](https://yandex.ru/efir?stream_channel=1550142789&stream_active=storefront) Session Viewer

![Riverbank](https://jing.yandex-team.ru/files/p45h/Yandex%20Riverbank.png)

## Установка среды разработки

1. Node.js and npm

   Убедитесь, что у Вас установлены ``node`` и ``npm``.
   
   >**Проверка ``node``**. Запустите в терминале команду ``node -v``. В случае, если ``node`` установлен, в терминале будет сообщение указывающее текущую версию, например ``v12.4.0``.

   >**Проверка ``npm``**. Запустите в терминале команду ``npm -v``. В случае, если ``npm`` установлен, в терминале будет сообщение указывающее текущую версию, например ``6.9.0``.

    Если у Вас нет команд ``node`` и ``npm``, то воспользуйтесь [Homebrew](https://treehouse.github.io/installation-guides/mac/homebrew) и запустите ``brew update && brew install node`` 

2. PostgreSQL

   Необходимо произвести подключение к удаленной БД

   Создайте папку ``configs`` в корне проекта

   Создайте файл ``configs/development.js`` и укажите там [username](https://yav.yandex-team.ru/secret/sec-01e6xv9dahqyyj9f259hb0r6yj/explore/versions) и [password](https://yav.yandex-team.ru/secret/sec-01e6xvcytz6x9e5fzpe4e9mxzp/explore/versions) от удаленной базы данных (формат смотрите в файле ``.config/default.js``)

3. Настройка YQL (YQL сейчас не используется - ходим напрямую в ClickHouse)

   Впишите YQL Token из [секрета](https://yav.yandex-team.ru/secret/sec-01e9rbet8ym42jnk46tb2nhr3c/explore/versions) в ``configs/development.js``

4. Yandex Internal Root CA Path
 
   Для запуска проекта необходимо проверить наличие сертификата YandexInternalRootCAPath в папке ``/usr/local/share/ca-certificates/``

   Если его нет, то по [ссылке](https://crls.yandex.net/YandexInternalRootCA.crt) качаем его и кладем в указанную выше папку

   Итоговый путь: ``/usr/local/share/ca-certificates/YandexInternalRootCA.crt``

5. Настройка STRM ClickHouse

   Секрет: https://yav.yandex-team.ru/secret/sec-01f8fss4pg896g98rp3kt6f4fn/explore/versions
   Секрет для testing: https://yav.yandex-team.ru/secret/sec-01f8f7nhmvscj5nwnjgarmsfxq/explore/versions

6. Настройка RUM ClikcHouse

   Секрет: https://yav.yandex-team.ru/secret/sec-01fvymcge3hrgjxtajap7enr63
   Хост: https://riverbank.clickhouse.error.yandex-team.ru

7. Настройка DRM ClickHouse

   Секрет: https://yav.yandex-team.ru/secret/sec-01g1jt8ny2f2r0jwjgzceqd53d
   Кластер: https://yc.yandex-team.ru/folders/foo00re08m0s670iusjg/managed-clickhouse/cluster/c685c744-b1d1-400a-81c9-e4c5ef4244d6/databases
   Порт для подключения: 8443

## Запуск среды разработки

1. Установите все зависимости командой ``npm install``.
   
2. Откройте два окна терминала
   
3. В первом терминале запустите ``npm run dev``, чтобы Webpack пересобирал исходники в режиме реального времени.

4. Во втором терминале создайте переменную окружения ```export NODE_ENV=development``` или добавьте ```NODE_ENV=development``` перед вызовом ```npm start```.

    4.1. Далее командой ``npm start`` запустите сервер Node.js.

5. Перейдите в браузере по адресу ```localhost:8100```.

## Деплой 
Пункты 1 - 4 проходятся единожды, тогда как 5 пункт нужно проходить всегда, когда Вы деплоите новые версии

1. Убедитесь, что у Вас установлен [Docker](https://docs.docker.com/docker-for-mac/install/).

    Вам необходимо запустить приложение Docker, чтобы загружать новые контейнеры в Yandex Registry

2. Подключитесь к Yandex Docker Registry
    
    Чтобы загрузить новый докер-образ в Yandex Docker Registry, Вам необходимо использовать [OAuth токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1), выпущенный в Яндексе. Если возникла проблема, то переходите к последней [инструкции](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)
    
    Далее авторизуемся при помощи следующих команд:

    ```
    docker login -u <login> --password-stdin registry.yandex.net
    <token_body><Enter>
    ^D (иногда может понадобиться еще один ^D, третий раз только не надо - выйдете из консоли)
    ```

    В случае ошибки смотрите в [инструкцию](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization).
   
3. Перед тем, как загружать новый образ, вам понадобятся разрешения участника. Если Вы еще не получили их, то можете запросить их на [Yandex IDM page](https://idm.yandex-team.ru/system/docker/roles#rf=1,rf-role=mJZWDLo7#user:funnyduck@docker/distribution/riverbank/contributor;;;Добавьте%20меня%20как%20contributor%20в%20registry,f-status=all,f-role=docker,sort-by=-updated,rf-expanded=mJZWDLo7)  

   Также понадобится доступ к [tools/nodejs](https://idm.yandex-team.ru/system/docker/roles#rf=1,rf-role=mJZWDLo7#docker/distribution/tools%7Cnodejs/viewer(fields:()),f-status=all,f-role=docker,sort-by=-updated,rf-expanded=mJZWDLo7), он используется как базовый образ  

5. Чтобы задеплоить образ, запустите следующие команды:

```make docker-build``` - собирает докер-образ на вашем компьютере и помечает его номером релизной версии

```make docker-push``` - отправляет собранный докер-образ в Yandex Docker Registry.

После этого достаточно пройти на нужный стейдж ([бета](https://deploy.yandex-team.ru/stage/riverbank-beta-stage/config) | [релиз](https://deploy.yandex-team.ru/stage/riverbank-stage/config)) и указать в конфигурации нужную версию.

## Счетчики ошибок

[Серверные и клиентские ошибки вместе](https://error.yandex-team.ru/projects/riverbank)

[Только серверные](https://error.yandex-team.ru/projects/riverbank?filter=runtime%20==%20nodejs)

[Только клиентские](https://error.yandex-team.ru/projects/riverbank?filter=runtime%20==%20browserjs)

## Мониторинги ошибок

Мониторинги настраиваются через мониторадо, чтобы добавить/изменить что-то, достаточно поправить [один файл](https://github.yandex-team.ru/mm-interfaces/riverbank/blob/master/.monitorado.yml), за деталями обращайтесь к [документации](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/monitorado) 
