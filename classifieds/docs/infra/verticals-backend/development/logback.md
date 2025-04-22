# Как переопределить стандартный конфиг logback-docker.xml

Сервисы, использующие [//common/zio/logging](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/common/zio/logging), запускаются с общими [настройками](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/common/zio/logging/resources). 
Для того, чтобы переопределить конфигурацию для своего сервиса, нужно положить к себе в ресурсы файл с именем **logback-override.xml** и содержимым внутри тега `<included>`  

Например:
```
<included>
    <logger name="my.custom.package" level="DEBUG" />
</included>
```