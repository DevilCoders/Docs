# Описание алертов
## Juggler проверки

### **yp.service_discovery.sd-requests-access-denied** {#1}

Тут еще нет описания :(

{% list tabs %}


- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-requests-access-denied)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}


### **yp.service_discovery.sd-requests-empty-responses-test** {#2}

Тут еще нет описания :(

{% list tabs %}


- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-requests-empty-responses-test)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}


### **yp.service_discovery.sd-requests-empty-responses** {#3}

Общее количество ответов с пустым списком endpoint-ов на запросы резолва по endpoint set id превышает какой-то числовой лимит

{% cut "Возможные причины и решения" %}

  ---
  
  Какой-то из сервисов делает запросы на пустые/несуществующие endpoint set-ы
  
  **Решение**. Посмотреть в логи и понять из какого сервиса приходят запросы. Спросить ожидаемое ли поведение, попросить так не делать :D
  
  **Пример**. [https://st.yandex-team.ru/SPI-35380](https://st.yandex-team.ru/SPI-35380)


{% endcut %}


{% cut "К кому можно обратиться" %}

**Информированные**: [ismagilas@](https://staff.yandex-team.ru/ismagilas), [azuremint@](https://staff.yandex-team.ru/azuremint)

{% endcut %}


{% list tabs %}


- Solomon

  * [Production clusters](https://solomon.yandex-team.ru/admin/projects/service_discovery/alerts/sd-requests-empty-responses)
  * [Testing clusters](https://solomon.yandex-team.ru/admin/projects/service_discovery/alerts/sd-requests-empty-responses-test)

- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-requests-empty-responses)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}


### **yp.service_discovery.sd-http-service-exceptions-occured** {#4}

Тут еще нет описания :(

{% list tabs %}


- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-http-service-exceptions-occured)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}


### **yp.service_discovery.sd-http-service-queue-overflow** {#5}

Тут еще нет описания :(

{% list tabs %}


- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-http-service-queue-overflow)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}


### **yp.service_discovery.sd-http-service-failed-queue-overflow** {#6}

Тут еще нет описания :(

{% list tabs %}


- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-http-service-failed-queue-overflow)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}


### **yp.service_discovery.sd-http-service-max-connections-reached** {#7}

Тут еще нет описания :(

{% list tabs %}


- Juggler

  * [Проверки](https://juggler.yandex-team.ru/aggregate_checks/?project=yp.service_discovery&query=service%3Dyp.service_discovery.sd-http-service-max-connections-reached)

- Nanny

  * [vla_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/vla_yp_service_discovery)
  * [sas_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_service_discovery)
  * [man_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/man_yp_service_discovery)
  * [msk_service_discovery](http://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_service_discovery)

{% endlist %}

