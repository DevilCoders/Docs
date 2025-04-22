## Local run

* Build dependencies
    ```
     mvn clean compile -pl auto-wizard -am
    ```

* Prepare local files
    ```
    mkdir -p /var/lib/search/auto2/ru/catalog-card
    mkdir -p /var/lib/yandex/auto2/ext-data
    mkdir -p /var/log/auto2/ru
    cp -R packages/yandex-auto2-ext-data/ext-data/ru /var/lib/yandex/auto2/ext-data
    cp datasources/testing/yandex-auto2-config-ru-testing/src/datasources.properties auto-wizard/src/main/resources/wizard-local.properties
    chmod -R 777 /var/lib/search/
    chmod -R 777 /var/lib/yandex/
    chmod -R 777 /var/log/auto2/ru/
    ```
  
* Copy datasources file from any test environment host, for example:
  
  ```
  scp back-rt-01-sas.test.vertis.yandex.net:/etc/yandex/vertis-datasources/datasources.properties /tmp && sudo mv /tmp/datasources.properties /etc/yandex/vertis-datasources/datasources.properties
  ```

* Run server (class `ru.yandex.auto.wizard.main.Main`) with such minimal VM-options list:
    ```
    -Xms8G -Xmx12G -Dauto.locale=ru -Dservice.name=auto2 -Dcomponent.name=wizard -Dmodule.name=auto2-wizard -Dhost.name=localhost
    ```
    and program arguments `classpath:wizard-core.xml `
