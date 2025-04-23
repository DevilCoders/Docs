# mbi-crm-proxy

1. Проперти, которые проект тянет с [гитхаба](https://github.yandex-team.ru/cs-admin/datasources-ng-dev/blob/master/development/etcd.yml), добавлены в `mbi-crm-proxy/src/main/properties.d/development/local-datasources.properties`
2. Генерируем проект:
```
ya ide idea -r ~/IdeaProjects/mbi-crm-proxy -l <arcadia_root>/market/mbi/mbi-crm-proxy
```
3. Создаем стартовую конфигурацию (В Idea `Edit configurations` -> `+` -> `Application`):
- main class: `ru.yandex.common.util.application.XmlAppContextMain`
- module: `mbi-crm-proxy`
- JRE: 11
- Рабочий пример VM Options:
```
-Dlog.dir=/Users/r-posokhin/IdeaProjects/mbi-crm-proxy/log
-Dlog4j2.configurationFile=classpath:log4j2.xml
-Dlog4j2.contextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector
-Doracle.net.tns_admin=/Users/r-posokhin
-Denvironment=development
-Dconfigs.path=/Users/r-posokhin/arc/arcadia/market/mbi/mbi-crm-proxy/src/main/properties.d/
```
