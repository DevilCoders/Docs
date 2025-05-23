{% if product == "yandex-cloud" %} 

# Управление расходами  

Существует несколько способов контролировать расходы на вычисления.

1. В Биллинге вы можете [настроить уведомления](../../billing/operations/budgets.md) о превышении установленного бюджета для сервиса {{ ml-platform-name }}. Бюджет не влияет на потребление: {{ ml-platform-name }} продолжит работу, даже если бюджет будет превышен.
1. В {{ ml-platform-name }} вы можете настроить пороги потребления для каталога или для одного проекта. После превышения порога потребления все вычисления в проекте или проектах каталога останавливаются. Пороги потребления для проекта и каталога задаются в [тарифицирующих юнитах](../pricing.md#unit).

{% endif %}

{% if product == "cloud-il" %}

# Ограничение используемых ресурсов

В {{ ml-platform-name }} вы можете настроить пороги потребления для каталога или для одного проекта. После превышения порога потребления все вычисления в проекте или проектах каталога останавливаются. Пороги потребления для проекта и каталога задаются в юнитах. 

{% endif %}

В качестве порогов потребления вы можете задать:

* Баланс `unit_balance` — общее количество юнитов, доступных для проекта или каталога. Каждое исполнение ячейки будет уменьшать баланс на то количество юнитов, которое необходимо для выполнения одной секунды вычислений выбранной [конфигурации](../concepts/configurations.md). Ячейки можно запускать до тех пор, пока баланс положительный. Если во время вычислений в одной из ячеек баланс станет меньше или равен нулю, все запущенные вычисления будут остановлены с предупреждением, что баланса проекта недостаточно.

* Ограничение на количество юнитов в час `max_units_per_hour`, которое может использовать проект. Если [цена за час](../pricing.md) для выбранной конфигурации при запуске вычислений превышает `max_units_per_hour`, ячейка не запустится. Если в процессе вычислений в ячейке текущее потребление проекта за час превысит `max_units_per_hour`, все ячейки с вычислениями будут остановлены.

* Ограничение на количество юнитов `max_units_per_execution`, доступных для одного вычисления. Если в процессе вычислений ячейка превысит установленное ограничение `max_units_per_execution`, она будет остановлена.

Ограничения независимы и могут быть назначены проекту или каталогу одновременно.

Для управления расходами потребуются следующие роли:
* посмотреть ограничения проекта — роль `{{ roles-datasphere-user }}`;
* установить ограничения проекта — роль `{{ roles-datasphere-admin }}`;
* посмотреть ограничения каталога — роль `{{ roles-viewer }}`; 
* установить ограничения каталога — роль администратора облака `{{ roles-admin }}`. 
 
Подробнее о ролях и управлении доступом в {{ ml-platform-name }} читайте в разделе [{#T}](../security/index.md).

#### См. также {#see-also}

* [{#T}](../operations/projects/custom-limits.md)
* [{#T}](../operations/projects/set-ds-budget.md)
