# Пользовательский CRM Маркета: Маркетинговый CRM

## Настройка проекта

1. Выполнить общую [настройку](../README.md)

1. Перенести из [Секретницы](https://yav.yandex-team.ru/secret/sec-01e9ysbvb4y7snnrjceg7txnss/explore/versions) в проект
   конфигурационные файлы, содержащие пароли:
   * `local.properties` надо положить в `src/main/properties.d/local`;
   * `tvm-local.json` надо положить в `src/main/conf/local`.

1. Настраиваем запуск приложения из idea.
   * В меню _Run->Edit Configurations..._ нажимаем '+' в левом верхнем углу;
   * В выпавшем списке выбираем _Application_;
   * В поле _Name_ указываем *campaign*;
   * В поле _Main class_ указываем `ru.yandex.market.crm.campaign.Server`;
   * В поле _VM Options_ указываем `-Djava.net.preferIPv6Addresses=true` ;
   * В поле _Working directory_ указываем `$MODULE_WORKING_DIR$` ;
   * В поле _Enviroment variables_
     указываем `PROPERTIES_DIR=_${user.home}_/arcadia/market/lilucrm/campaign/src/main/properties.d/` ;
   * В поле _Use classpath of module_ указываем *campaign*.

1. Для компиляции JS и работы вэб-интерфейса (больше подробностей в `webapp/readme.md`):
   * В директории `webapp` создаем симлинк на ресурсы модуля `mcrm_core`. Для этого достаточно перейти в `webapp` и
     выполнить там `ln -s ../../mcrm_core/src/main/resources`.
   * Не уходя из `webapp`, выполняем `yarn install` для установки JS-зависимостей.
   * Запускаем скрипт `bin/watch.sh`
