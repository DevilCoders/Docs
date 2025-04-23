## Локальный запуск стрельбы

Для того, чтобы запустить генератор нагрузки для nwsmtp локально для отладки или модификации нужно:
* Скачать инициатор jMeter, используемый в стрельбе. Он доступен как [ресурс](https://proxy.sandbox.yandex-team.ru/1753798106) с архивом. 
  Архив нужно распаковать в отдельную директорию на вашем компьютере.
* Установить на машину Java8.
* Переопределить переменную окружения $JAVA_HOME на каталог с JRE8. Для этого можно воспользоваться утилитой java_home:
```bash
$ /usr/libexec/java_home -V
    ...
    1.8.0_252, x86_64:	"AdoptOpenJDK 8"	/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
    1.8.0_252, x86_64:	"AdoptOpenJDK (OpenJ9, JRE) 8"	/Library/Java/JavaVirtualMachines/adoptopenjdk-8-openj9.jre/Contents/Home
    1.8.0_252, x86_64:	"AdoptOpenJDK (JRE) 8"	/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jre/Contents/Home
    1.8.0_252, x86_64:	"AdoptOpenJDK (OpenJ9) 8"	/Library/Java/JavaVirtualMachines/adoptopenjdk-8-openj9.jdk/Contents/Home
    ...
$ export $JAVA_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-8-openj9.jre/Contents/Home
```
* В отдельную директорию скопировать из аркадии:
а. Нужный jmx файл;
б. Файл с сертификатами YandexInternalCA.keystore;
в. Файл csv с авторизационными данными;
г. Создать файл sessions c содержимым ```short,2``` или другим, на собственное усмотрение. Также можно задействовать утилиту sessions.py.
д. Скачать [файл с сообщениями](https://proxy.sandbox.yandex-team.ru/1753862036) 
* Запустить генератор нагрузки:
```bash
$ _JMETER_PATH_/jmeter-4.0/bin/jmeter-large -t _JMX_PATH_/smtp-sessions.jmx -Jjmeter.save.saveservice.connect_time=true -Djavax.net.ssl.trustStore=YandexInternalCA.keystore -Djava.net.preferIPv6Addresses=true
```
Если все было сделано корректно, то должно открыться окно jMeter с настройками теста. В этом окне следует активировать секции **User Defined Variables** и **View Results Tree**, в секции **User Defined Variables** в полях **ammo** и **users** указать путь до файлов с сообщениями и пользовательскими данными соответсвенно или просто наименования файлов если они расположены в директории из которой запускается jMeter. После можно запустить генератор. Результаты теста будут отображаться в секции **View Results Tree**. 
Для корректного проведения теста должен быть доступ с клиентского компьютера до нагрузочного стенда по портам 25 и 465. 