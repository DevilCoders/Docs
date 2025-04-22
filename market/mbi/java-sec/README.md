### Локальная сборка и запуск тестов
[ya.make](https://wiki.yandex-team.ru/yatool/make/) 

### Пример VM Options для локального запуска java-sec-http-proxy (поправить под себя)
```
-Dlog.dir=/Users/r-posokhin/IdeaProjects/java-sec/java-sec-http-proxy/log
-Dlog4j2.configurationFile=classpath:log4j2.xml
-Dlog4j2.contextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector
-Doracle.net.tns_admin=/Users/r-posokhin
-Denvironment=local
-Dconfigs.path=/Users/r-posokhin/arc/arcadia/market/mbi/java-sec/java-sec-http-proxy/src/main/properties.d
-Dbean.file=classpath:bean.xml
```

###Деплой компонентов на dev среду (неактуально)
**Для бэкенда (editor и http-proxy)**

* Из [списка зарезервированных за пользователем портов](https://wiki.yandex-team.ru/MBI/Development/new_developer/#rezervirovanieportov) необходимо выбрать:
    * порт для отладки **DEBUG_PORT**.
    * порт для HTTP **HTTP_PORT**.

Далее необходимо узнать свой **UID** в Паспорте. Для этого на **braavos**'е выполняем следующий http-запрос, заменив <login> на свой логин: 

``
curl -s "http://blackbox-mimino.yandex.net/blackbox?method=userinfo&userip=127.0.0.1&login=<login>"
``

В ответе на запрос кроме прочей информации будет присутствовать UID.

* В каждом компоненте в папке `development` 
создать файл `servant-local.properties` 
со следующим содержимым:

```
http.port=<your-port>
debug.port=<your-debug-port>
environmentJvmArgs=-Dspring.profiles.active=development -Doracle.net.tns_admin=/etc/oracle
passport.uid=<UID>
```


>- **Для чего нужен UID?**
>- Т.к. dev-сервер находится в домене yandex.net, a не yandex.ru, то для него недоступна cookie ``Session_id``, 
а поэтому любой запрос к бэку будет возвращать ответ **ERROR_NO_AUTH**. 
Поэтому на dev-среде сначала производится попытка достать UID из property под названием `passport.uid`.


* Залить каждый компонент на braavos<br> 
Из корня проекта:
```$xslt
../mbi-tools/uploadToDev.sh <module_name>
```

* Стартануть компоненты 
```
ssh braavos
cd dev/<component-name>
./bin/<component-name>-start.sh
```
<a name="http-proxy"></a>

**Для фронта (editor-ui)**

* Запустить сервер приложения на braavos. Фронт будет доступен по адресу `http://braavos.market.yandex.net:<HTTP_PORT>`

**Для отладки фронта (editor-ui)**

* Запустить сервер приложения на braavos.

* Запустить CodeServer - **не адаптировано после переезда в аркадию, TBD.**
В консоли будет выведен адрес, по которому можно заходить в браузер. 
На странице будет предложено добавить ссылки  ``Dev Mode On |  Dev Mode Off`` на панель закладок и перейти к файлам, 
которые можно скомпилировать. Если сейчас компилировать  ``editor.html`` , то он успешно скомпилируется, 
но запросы к бэку посылаться не будут, т.к. CodeServer не знает как обрабатывать эти запросы.

* Локально или в докер-контейнере поднять nginx-сервер, 
который будет проксировать запросы js файлов на CodeServer, а ручки  java-sec на braavos.
Для того чтобы локально поднять nginx-сервер нужно установить nginx, и написать для него файл ``nginx.conf`` 
с конфигурацией (заменить <HTTP_PORT>):


```
events {
    worker_connections  512;
}

http {
  server {
      listen       <HTTP_PORT>;
      server_name  localhost;

      location ~^/(.+)Service$ {
        proxy_pass http://braavos.market.yandex.net:<HTTP_PORT>;
      }

      location / {
          proxy_pass http://localhost:9876/ru.yandex.market.security.ui.Editor/;
      }
  }
}
```

* После этого запустить nginx-сервер, указав ему абсолютный путь до конфигурационного файла:
 ``nginx -c <path_config_file>``
Теперь можно зайти в браузере по адресу `http://localhost:<HTTP_PORT>/editor.html` 
и нажать на добавленную ранее закладку  Dev Mode On , чтобы перекомпилировать JS код, 
если он не обновился автоматически.

**Получить права**
* Получить id (passport_id): 

```
curl -s "http://blackbox-mimino.yandex.net/blackbox?method=userinfo&userip=127.0.0.1&login=<yndx-login>"
```

В респонсе:

```
<uid hosted="0"><id></uid>
```
* Проверить наличие прав, в случае необходимости накатить через консоль
```
insert into java_sec.static_domain_auth values (4, <id>, 'SECURITY_MANAGER');
insert into JAVA_SEC.domain_admins values(1, <id>);
insert into JAVA_SEC.domain_admins values(2, <id>);
insert into JAVA_SEC.domain_admins values(3, <id>);
insert into JAVA_SEC.static_auth values(JAVA_SEC.s_id.nextval, <id>, 'SECURITY_MANAGER');
insert into JAVA_SEC.static_auth values(JAVA_SEC.s_id.nextval, <id>, 'YA_STAFF'); 
```
