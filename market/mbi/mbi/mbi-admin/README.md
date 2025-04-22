# Информация о модуле
Актуальную информацию о модуле смотри на [wiki](https://wiki.yandex-team.ru/mbi/newdesign/components/mbi-admin/).

## Локальный запуск из IDEA

###1. Настраиваем получение инфы о пользователе с паспорта (уже сделано)

Админка ходит в паспорт за инфой о текущем пользователе по URL
```
blackbox.url=http://blackbox-mimino.yandex.net/blackbox
```
Т.к. с локальных машинок сюда доступа нет, то следует настроить прокси на **braavos**,
например через сервер **nginx**.

В Ubuntu он устанавливается командой `sudo apt install nginx`

Далее редактируем файлик /etc/nginx/nginx.conf
```
sudo nano /etc/nginx/nginx.conf
```
Добавляем конфигурацию прокси в раздел http:
```
http {
    ...
    server {
        listen       7643;
        listen       [::]:7643;
        location / {
            proxy_pass http://blackbox-mimino.yandex.net:80;
        }
    }
    ...
}
```
и рестартуем nginx
```
sudo nginx -s reload
```

###2. Правим properties (уже сделано)

В компоненте меняем в файле servant-local.properties:
```properties
blackbox.url=http://braavos.market.yandex.net:7643/blackbox
passport.uid=<uid своего yndx-пользователя>
```
Если не знаем свой UID для yndx-пользователя, его можно узнать тут https://api.passport.yandex.ru/accounts.
На данный момент в файле эти поля уже выставлены и стоит uid для для юзера `yndx-skiftcha-mbi-developer`,
тк не все yndx-юзеры проросли на braavos.

###3. Запускаем админку в IDEA

Чтобы `ya-idea` сгенерировала gwt странички нужно выставить
```
EXTRA_YA_MAKE_PARAMS="-D=YA_IDEA_GWT"
```
в ~/.ya/direct-ya-idea.overrides.sh и перегенерить проект, иначе можно получить 404 вместо главной страницы.

Настраиваем run-config в IDEA:
1. Main class `ru.yandex.common.util.application.XmlAppContextMain`
2. Classpath `mbi-admin`
3. Working dir `$MODULE_WORKING_DIR$`LazyJmxMetricsProvider
4. Vm properties
```properties
-Denvironment=local
-Dbean.file=classpath:bean.xml
-Dconfigs.path=/home/churlyaev-p/arc/arcadia/market/mbi/mbi/mbi-admin/src/main/properties.d
-Dlog4j2.configurationFile=/home/churlyaev-p/arc/arcadia/market/mbi/mbi/mbi-admin/src/main/conf/log4j2.xml
-Dlog4j2.contextSelector=org.apache.logging.log4j.core.selector.ClassLoaderContextSelector
-Dlog.dir=/home/churlyaev-p/IdeaProjects/mbi/logs/mbi-admin
-javaagent:/home/churlyaev-p/IdeaProjects/mbi/contrib/java/org/aspectj/aspectjweaver/1.9.2/aspectjweaver-1.9.2.jar
-Dservant.home.dir=src/main/properties.d
-Dspring.profiles.active=development,transparent_security_filter
-Dspring.context.initializers=ru.yandex.market.core.initializer.LocalStartContextInitializer
-Dhttp.port=4500
-Djava.library.path=/home/churlyaev-p/IdeaProjects/mbi/dlls
-Djava.awt.headless=true
```
В свойствах меняем
 - путь `/home/churlyaev-p` на свою домашнюю директорию,
 - путь `/arc/arcadia` - на свою директорию примонтированной аркадии
 - путь `/IdeaProjects/mbi` на свою папку с проектом mbi в идее
 - свойство `http.port` на свой желаемый порт

После этого по пути http://localhost:4500/admin.html (порт из `http.port`) админка должна стать доступна.

###Возможные проблемы

Если при заходе на страницу сразу выбрасывает на страницу логина в паспорт - возможно, для выбранного UID (п.2) не хватает прав. Тогда можно спросить
их в чате MBI, либо взять какой-то ID юзера с ролью admin из таблицы **SHOPS_WEB.USER_ROLES** на деве в качестве своего UID.

##Запуск GWT Super Dev Mode
Super Dev Mode - отладочный режим GWT, позволяющий пересобирать приложение "на лету",
по одной кнопке, без полной перекомпиляции проекта. Такой режим позволяет быстрее отлаживать приложение и экономить время.

Super Dev Mode можно запускать как на локалке, так и на админке на **braavos** - в любом случае это делается из окна браузера

Для запуска выполняем следующее.

###1. Качаем GWT SDK 2.9.0
[Отсюда.](https://storage.googleapis.com/gwt-releases/gwt-2.9.0.zip)

Распаковываем его в произвольную папку

###2. Прописываем путь к SDK в переменной среды
```shell
export GWT_HOME=<путь к нашей директории SDK>
```

Для постоянного эффекта стоит добавить эту строчку в конец файла `~/.bashrc`
###3. Запускаем сервер
Запускается скриптом из-под папки mbi-admin-ui
```shell
cd mbi-admin-ui
sh devMode.sh
```
Если запускаете сервер не в первый раз, и при этом он кричит на ошибки, вроде
**cannot resolve class to a type** на случайные классы - стоит зайти в папку /tmp и удалить в ней
всё, что начинается с **gwt** - любые файлы и папки, что могло закэшироваться.

###4. (Для первого запуска) делаем закладки на dev mode
Заходим по адресу http://localhost:9876 и перетаскиваем огромные
квадраты "Dev Mode On" и "Dev Mode Off" себе на панель закладок браузера,
так чтобы получились кнопки

###5. Запускаем дев мод в приложении
У нас должно быть уже запущенное приложение через идею (см. предыдущую главу).
Заходим по адресу приложения с выбранным портом, и нажимаем в закладках браузера `Dev mode on`.
После этого нам предложат скомпилировать проект.

Далее после любых изменений в коде нажимаем Dev Mode On -> Compile,
и все изменения в коде должны автоматически подтянуться на текущую страницу.

##Возникли проблемы
О текущих проблемах пишите @churlyaev-p.
