# Триггерная платформа

## Настройка проекта

**1**. Выполнить общую [настройку](../README.md)

**2**. Перенести из [wiki](https://wiki.yandex-team.ru/Market/Development/lilucrm/secrets/#mcrm) в проект конфигурационные файлы, содержащие пароли.
Только кладём их не в `campaign/src/main/properties.d/local`, а в `triggers_platform/src/main/properties.d/local`.

**3**. Добавить настройки для упрощения запуска в `triggers_platform/src/main/properties.d/local/local.properties`:

```
bpm.enableDbHistory=false
```

**4**. Настроить запуск приложения из idea.

 * В меню _Run->Edit Configurations..._ нажимаем '+' в левом верхнем углу;
 * В выпавшем списке выбираем _Application_;
 * В поле _Name_ указываем `triggers_platform`;
 * В поле _Main class_ указываем `ru.yandex.market.crm.triggers.Server`;
 * В поле _VM Options_ указываем `-Djava.net.preferIPv6Addresses=true` ;
 * В поле _Working directory_ указываем `$MODULE_WORKING_DIR$` ;
 * В поле _Enviroment variables_ указываем `PROPERTIES_DIR=_${user.home}_/arcadia/market/lilucrm/triggers_platform/src/main/properties.d/` ;
 * В поле _Use classpath of module_ указываем `triggers_platform`.
