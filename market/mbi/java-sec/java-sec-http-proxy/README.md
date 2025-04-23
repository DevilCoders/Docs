#### Пример рабочего конфига для локального запуска:

mainClass: `ru.yandex.common.util.application.XmlAppContextMain`<br>
Working directory: `/Users/r-posokhin/IdeaProjects/java-sec`<br>
JRE: `11`<br>
VM options:
```
-Dlog.dir=/Users/r-posokhin/IdeaProjects/java-sec/java-sec-http-proxy/log
-Dlog4j2.configurationFile=classpath:log4j2.xml
-Dlog4j2.contextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector
-Doracle.net.tns_admin=/Users/r-posokhin
-Denvironment=local
-Dconfigs.path=/Users/r-posokhin/arc/arcadia/market/mbi/java-sec/java-sec-http-proxy/src/main/properties.d
-Dbean.file=classpath:bean.xml
```