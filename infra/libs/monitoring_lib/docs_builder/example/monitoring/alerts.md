# Описание алертов

### **sst_files_size_limit_usage** {#1}

Достигнут некоторый % от лимита на суммарный размер sst файлов в реплике

{% cut "Возможные причины и решения" %}

  ---
  
  Произошло уплотнение данных в реплике. В этом случае будет краткий скачок размера (т.к. создались файлы на размер уплотнения) и откат до такого же или меньше значения (удалились старые).
  
  **Решение**. Безобидный момент т.к. не может выйти за общий лимит (но это не точно)

  ---
  
  На самом деле, достигнут этот самый % от лимита
  
  **Решение**. Тогда надо либо поднять %, либо общий лимит


{% endcut %}


{% cut "К кому можно обратиться" %}

**Aвторы**: [azuremint@](https://staff.yandex-team.ru/azuremint), [darkmint@](https://staff.yandex-team.ru/darkmint)
**Информированные**: [whitemint@](https://staff.yandex-team.ru/whitemint)

{% endcut %}


{% list tabs %}


- Docs

  * [https://docs.yandex-team.ru/yp-service-discovery/](https://docs.yandex-team.ru/yp-service-discovery/)

- Nanny

  * [msk_yp_dns](https://nanny.yandex-team.ru/ui/#/services/catalog/msk_yp_dns)
  * [sas_yp_dns](https://nanny.yandex-team.ru/ui/#/services/catalog/sas_yp_dns)

- You_tube

  * [nggyp](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

- Other

  * [abc](https://abc.yandex-team.ru/services/service_discovery/)

{% endlist %}


### **empty_alert** {#2}

:(((
