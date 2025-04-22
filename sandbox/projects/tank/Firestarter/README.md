Задача проведения нагрузочного теста
====
Выполняет проверку заданных условий теста, подготовительные действия, в случае их необходимости, и непосредственный запуск 
В качестве параметров настройки принимает:
- Dry run - Флаг выполнения задачи без непосредственного запуска нагрузочного теста, с целью проверить конфтгурацию и заданные условия проведения теста;
- Wait finish - Флаг инструкции ожидания завершения теста. В противном случае задача завершится по факту получения идентификатора стрельбы;
- Tank config - Конфигурация нагрузочного теста. В yaml формате;
- Monitoring config - Конфигурация для сбора мониторинга через плагин Telegraf. В xml формате.

В качестве выходных параметров задача возвращает статус завершения и идентификатор стрельбы в [Lunapark](https://lunapark.yandex-team.ru).

### Цель нагрузки (target)
Значение может быть указано в  в виде:
- Доменного имени;
- IPv4 или IPv6 адреса;
Такой способ указания допускается в любом, соответствующем для этого параметре конфигурации.
Для указания в неявном виде или в виде группового объединения хостов предлагается использовать раздел `metaconf.firestarter` и поля `target` и `target_port` конфигурации стрельбы. К таким вариантам относятся:
- Сервис в RTC - с указанием наименования сервиса, а также группы опционально;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        target: nanny:overload-front-production-yp
  ```
- Проект в Deploy - с указанием наименований stage, а также deploy_unit и datacenter опционально;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        target: deploy:lunapark-develop.lunapark-django.iva
        target_port: 80
  ```
- Output параметр другой Sandbox задачи - с указанием типа задачи, её тегов и нужного output параметра;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        target: sandbox.GENERATE_YAPPY_BETA.release:release_goods_backend,rm_ci.new_beta_url
        target_port: 80
  ```
Отдельно стоит отметить:
- В самописных генераторах на Pandora, BFG или jMeter цель может быть указана в любом поле, поэтому для таких случаев, а также для случая использования опции config_file для генератора на Pandora, значение цели теста устанавливается в строку `in_config`.

### Источник нагрузки (tank) 
Значение возможно указать в виде: 
- Доменного имени 
- IPv4 или IPv6 адреса
- Список из значений в указанных выше форматах.
В таком виде допускается указание источника теста в полях `uploader.meta.use_tank` и `metaconf.firestarter.tank`. 
В поле `metaconf.firestarter.tank` можно указывать для источника теста значения в неявном и групповом виде:
- Сервис в RTC - с указанием наименования сервиса, а также группы опционально;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        tank: nanny:production_yandex_tank
  ```
- Проект в Deploy - с указанием наименований stage, а также deploy_unit и datacenter опционально;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        tank: deploy:Yandextank_manual-testing.tank.myt
        tank_port: 8083
  ```
- Значение `common` для использования железных общественных танков;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        tank: common
  ```
- Значение `sandbox` для использования специализированной sandbox задачи;
**Пример**
  ```yaml
    metaconf:
      enabled: true
      package: yandextank.plugins.MetaConf
      firestarter:
        tank: sandbox
  ```

Отдельно стоит отметить случай кроссдц тестов. Мы не рекомендуем безпричинно проводить такие тесты и блокируем их на общественных танках.
Если Вам все же требуется провести такое тестирование (например, необходимо подать нагрузку через балансировщик), то сделать это можно: 
- через строго указанный танк дополнительно указав в поле `metaconf.firestarter.dc` значение `cross`;
- через танк `sandbox` с указанием в поле `metaconf.firestarter.dc` датацентра, в котором будет запущена дочерняя задача.

Стоит отметить, что нагрузочные тесты через самописные генераторы и использование поля `config_file` в настройках `Pandora` приравниваются к кроссдц и также запрещены на общесвенных танках.