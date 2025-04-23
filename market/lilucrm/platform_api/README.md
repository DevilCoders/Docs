# Пользовательский CRM Маркета: Платформа CRM (API)

## Настройка проекта

1. Выполнить общую [настройку](../README.md)

1. Перенести из [wiki](https://wiki.yandex-team.ru/Market/Development/lilucrm/secrets/#platformacrm) в проект конфигурационные
   файлы, содержащие пароли.
   
1. Настраиваем запуск приложения из idea.
    * В меню _Run->Edit Configurations..._ нажимаем '+' в левом верхнем углу;
    * В выпавшем списке выбираем _Application_;
    * В поле _Name_ указываем *platform-api*;
    * В поле _Main class_ указываем *ru.yandex.market.crm.platform.api.Server*;
    * В поле _VM Options_ указываем *-Djava.net.preferIPv6Addresses=true* ;
    * В поле _Working directory_ указываем *$MODULE_WORKING_DIR$* ;
    * В поле _Enviroment variables_ указываем *PROPERTIES_DIR=_${user.home}_/arcadia/market/lilucrm/platform_api/src/main/properties.d/* ;
    * В поле _Use classpath of module_ указываем *platform-api*.
