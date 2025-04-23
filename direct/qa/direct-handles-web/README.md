###direct-handles-rest
Бекэнд для рукояточника

###Запуск локально

Скачать в корень проекта jetty-starter.jar из https://jenkins-direct.qart.yandex-team.ru/job/applications/job/jetty-starter/
```
mvn clean package
sudo docker build -t registry.yandex.net/direct-qa/applications:direct-handles-rest-<ДАТА> .
sudo docker run --net=host -e QLOUD_HTTP_PORT=1786 registry.yandex.net/direct-qa/applications:direct-handles-rest-<ДАТА>
```
Альтернативно можно собрать проект через Maven в Idea (Maven -> Direct Handles Webapp Beans -> clean | package,
Maven -> Direct Handles Webapp rest-services ->  clean | package)

Для дебага нужно указать ```-DDEBUG_PORT=1234``` и подлючаться remote debugger по этому порту.
Обращаться к приложению необходимо по порту ```1786```

Также можно просто запустить ```app-start.sh```
```
mvn clean package
export DEBUG_PORT=1234
export SUSPEND=y
bash app_start.sh
```

Альтернативно можно запускать JettyDebugStarter из direct-handles-rest и ходить браузером на порт 9002.
В переменной WAR_PATH необходимо указать полный путь к war-файлу.
Нужно помнить, что .war нужно пересобирать (mvn clean package) при каждом изменении в коде.

Для получения логов запуска скриптов транспорта нужно задать две переменных окружения
- QLOUD_TVM_SECRET - секрет для рукояточника
- QLOUD_TVM_SELF_ID - TVM ClientID рукояточника

Значения этих переменных берутся из Секретницы
https://yav.yandex-team.ru/secret/sec-01e1h5ksprb91vtqjtzpcsdfff

###Заливака образа в registry

```
sudo docker push registry.yandex.net/direct-qa/applications:direct-handles-rest-<ДАТА>
```

###Апдейт в deploy

приложение живет тут</br>
https://deploy.yandex-team.ru/projects/direct-infra</br>
Есть 3 окружения ```direct-handles-test```,```direct-handles-prod``` и ```direct-handles-scriptrunner```. Для обновления необходимо зайти в окружение, нажать update для контейнера и выбрать тег ```direct-handles-rest-<ДАТА>```</br>
Подробнее https://docs.yandex-team.ru/direct-dev/guide/jeri/ts-ext-tools-update

###Совместимость с Java 9+

Её нет. При сборке можно указать путь до jre8.
