---
editable: false
---

# Метод list
Возвращает список кластеров Kubernetes в указанном каталоге.
 

 
## HTTP-запрос {#https-request}
```
GET https://mks.api.cloud.yandex.net/managed-kubernetes/v1/clusters
```
 
## Query-параметры {#query_params}
 
Параметр | Описание
--- | ---
folderId | Обязательное поле. Идентификатор каталога для получения списка кластеров Kubernetes. Чтобы получить идентификатор каталога, используйте запрос [list](/docs/resource-manager/api-ref/Folder/list).
pageSize | Максимальное количество результатов на странице ответа на запрос. Если количество результатов больше чем [pageSize](/docs/managed-kubernetes/api-ref/Cluster/list#query_params) , сервис вернет значение [nextPageToken](/docs/managed-kubernetes/api-ref/Cluster/list#responses), которое можно использовать для получения следующей страницы. Значение по умолчанию: 100.  Допустимые значения — от 0 до 1000 включительно.
pageToken | Токен страницы. Установите значение `page_token` равным значению поля [nextPageToken](/docs/managed-kubernetes/api-ref/Cluster/list#responses) предыдущего запроса, чтобы получить следующую страницу результатов.  Максимальная длина строки в символах — 100.
filter | Параметры фильтрации ресурсов в ответе. В параметрах фильтрации указываются: 1. Имя поля. В настоящее время фильтрация осуществляется только по полю [Cluster.name](/docs/managed-kubernetes/api-ref/Cluster#representation). 2. Оператор. Операторы `=` или `!=` для одиночных значений, `IN` или `NOT IN` для списков значений. 3. Значение. Значение длиной от 1 до 61 символов, совпадающее с регулярным выражением `^[a-z][-a-z0-9]{1,61}[a-z0-9]$`.  Максимальная длина строки в символах — 1000.
 
## Ответ {#responses}
**HTTP Code: 200 - OK**

```json 
{
  "clusters": [
    {
      "id": "string",
      "folderId": "string",
      "createdAt": "string",
      "name": "string",
      "description": "string",
      "labels": "object",
      "status": "string",
      "health": "string",
      "networkId": "string",
      "master": {
        "version": "string",
        "endpoints": {
          "internalV4Endpoint": "string",
          "externalV4Endpoint": "string"
        },
        "masterAuth": {
          "clusterCaCertificate": "string"
        },
        "versionInfo": {
          "currentVersion": "string",
          "newRevisionAvailable": true,
          "newRevisionSummary": "string",
          "versionDeprecated": true
        },
        "maintenancePolicy": {
          "autoUpgrade": true,
          "maintenanceWindow": {

            // `clusters[].master.maintenancePolicy.maintenanceWindow` включает только одно из полей `anytime`, `dailyMaintenanceWindow`, `weeklyMaintenanceWindow`
            "anytime": {},
            "dailyMaintenanceWindow": {
              "startTime": {
                "hours": "integer",
                "minutes": "integer",
                "seconds": "integer",
                "nanos": "integer"
              },
              "duration": "string"
            },
            "weeklyMaintenanceWindow": {
              "daysOfWeek": [
                {
                  "days": [
                    "string"
                  ],
                  "startTime": {
                    "hours": "integer",
                    "minutes": "integer",
                    "seconds": "integer",
                    "nanos": "integer"
                  },
                  "duration": "string"
                }
              ]
            },
            // конец списка возможных полей`clusters[].master.maintenancePolicy.maintenanceWindow`

          }
        },

        // `clusters[].master` включает только одно из полей `zonalMaster`, `regionalMaster`
        "zonalMaster": {
          "zoneId": "string",
          "internalV4Address": "string",
          "externalV4Address": "string"
        },
        "regionalMaster": {
          "regionId": "string",
          "internalV4Address": "string",
          "externalV4Address": "string"
        },
        // конец списка возможных полей`clusters[].master`

      },
      "ipAllocationPolicy": {
        "clusterIpv4CidrBlock": "string",
        "serviceIpv4CidrBlock": "string"
      },
      "serviceAccountId": "string",
      "nodeServiceAccountId": "string",
      "releaseChannel": "string",
      "networkPolicy": {
        "provider": "string"
      },
      "gatewayIpv4Address": "string"
    }
  ],
  "nextPageToken": "string"
}
```

 
Поле | Описание
--- | ---
clusters[] | **object**<br><p>Кластер Kubernetes.</p> 
clusters[].<br>id | **string**<br><p>Идентификатор кластера Kubernetes.</p> 
clusters[].<br>folderId | **string**<br><p>Идентификатор каталога, которому принадлежит кластер Kubernetes.</p> 
clusters[].<br>createdAt | **string** (date-time)<br><p>Время создания.</p> <p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
clusters[].<br>name | **string**<br><p>Имя кластера Kubernetes.</p> 
clusters[].<br>description | **string**<br><p>Описание кластера Kubernetes. Длина описания должна быть от 0 до 256 символов.</p> 
clusters[].<br>labels | **object**<br><p>Метки ресурса в формате ``key:value``. Максимум 64 метки на ресурс.</p> 
clusters[].<br>status | **string**<br>Статус кластера Kubernetes.<br><ul> <li>PROVISIONING: Кластер Kubernetes ожидает выделения ресурсов.</li> <li>RUNNING: Кластер Kubernetes запущен.</li> <li>RECONCILING: Кластер Kubernetes согласовывается.</li> <li>STOPPING: Кластер Kubernetes останавливается.</li> <li>STOPPED: Кластер Kubernetes остановлен.</li> <li>DELETING: Кластер Kubernetes удаляется.</li> <li>STARTING: Кластер Kubernetes запускается.</li> </ul> 
clusters[].<br>health | **string**<br>Состояние кластера Kubernetes.<br><ul> <li>HEALTHY: Кластер Kubernetes работает нормально.</li> <li>UNHEALTHY: Кластер Kubernetes не работает и не может выполнять свои основные функции.</li> </ul> 
clusters[].<br>networkId | **string**<br><p>Идентификатор облачной сети, к которой принадлежит кластер Kubernetes.</p> 
clusters[].<br>master | **object**<br>Свойства мастера для кластера Kubernetes.<br>
clusters[].<br>master.<br>version | **string**<br><p>Версия компонентов Kubernetes, которая запущена на мастере.</p> 
clusters[].<br>master.<br>endpoints | **object**<br>Эндпойнт мастера. Эндпойнты состоят из схемы и порта (т. е. `https://ip-address:port`) и могут использоваться клиентами для связи с API Kubernetes кластера Kubernetes.<br>
clusters[].<br>master.<br>endpoints.<br>internalV4Endpoint | **string**<br><p>Внутренний эндпойнт, который может использоваться для подключения к мастеру из облачных сетей.</p> 
clusters[].<br>master.<br>endpoints.<br>externalV4Endpoint | **string**<br><p>Внешний эндпойнт, который может использоваться для доступа к API кластера Kubernetes из интернета (вне Облака).</p> 
clusters[].<br>master.<br>masterAuth | **object**<br>Параметры, используемые для аутентификации мастера.<br>
clusters[].<br>master.<br>masterAuth.<br>clusterCaCertificate | **string**<br><p>Публичный PEM-закодированный сертификат, подтверждающий подлинность кластера Kubernetes.</p> 
clusters[].<br>master.<br>versionInfo | **object**<br>Подробная информация о версии Kubernetes, которая запущена на мастере.<br>
clusters[].<br>master.<br>versionInfo.<br>currentVersion | **string**<br><p>Текущая версия Kubernetes, формат: major.minor (например, 1.15).</p> 
clusters[].<br>master.<br>versionInfo.<br>newRevisionAvailable | **boolean** (boolean)<br><p>Новые версии могут включать патчи Kubernetes (например, 1.15.1 -&gt; 1.15.2), а также некоторые обновления внутренних компонентов — новые функции или исправления ошибок в конкретных компонентах Яндекса на мастере или на узлах.</p> 
clusters[].<br>master.<br>versionInfo.<br>newRevisionSummary | **string**<br><p>Описание изменений, которые будут применены при обновлении до последней версии. Пусто, если поле ``new_revision_available`` имеет значение ``false``.</p> 
clusters[].<br>master.<br>versionInfo.<br>versionDeprecated | **boolean** (boolean)<br><p>Текущая версия устарела, компонент кластера Kubernetes (мастер или группа узлов) должен быть обновлен.</p> 
clusters[].<br>master.<br>maintenancePolicy | **object**<br>Политика обновления мастера.<br>
clusters[].<br>master.<br>maintenancePolicy.<br>autoUpgrade | **boolean** (boolean)<br><p>Если установлено значение ``true``, автоматическое обновление устанавливается без участия пользователя в заданный промежуток времени. Если установлено значение ``false``, автоматическое обновление отключено.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow | **object**<br><p>Настройки окна обновления. Обновление начнется в указанное время и продлится не более указанного времени. Время устанавливается в формате UTC.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>anytime | **object**<br>Обновление мастера в любое время. <br>`clusters[].master.maintenancePolicy.maintenanceWindow` включает только одно из полей `anytime`, `dailyMaintenanceWindow`, `weeklyMaintenanceWindow`<br><br>
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow | **object**<br>Обновление мастера в любой день в течение указанного временного окна. <br>`clusters[].master.maintenancePolicy.maintenanceWindow` включает только одно из полей `anytime`, `dailyMaintenanceWindow`, `weeklyMaintenanceWindow`<br><br>
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow.<br>startTime | **object**<br><p>Обязательное поле. Время начала окна обновлений, указывается в часовом поясе UTC.</p> <p>Время суток. Дата и часовой пояс либо не учитываются, либо задаются в других местах.</p> <p>API может разрешить использование високосной секунды.</p> <p>Связанные типы: <a href="https://github.com/googleapis/googleapis/blob/master/google/type/date.proto">google.type.Date</a> и <a href="https://github.com/protocolbuffers/protobuf/blob/master/src/google/protobuf/timestamp.proto">google.protobuf.Timestamp</a>.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow.<br>startTime.<br>hours | **integer** (int32)<br><p>Часы. Допустимые значения: от 0 до 23.</p> <p>API может разрешить использовать значение в формате &quot;24:00:00&quot; в требующих этого сценариях (например, для указания времени закрытия учреждения).</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow.<br>startTime.<br>minutes | **integer** (int32)<br><p>Минуты. Допустимые значения: от 0 до 59.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow.<br>startTime.<br>seconds | **integer** (int32)<br><p>Секунды. Стандартные допустимые значения: от 0 до 59.</p> <p>API может разрешить использовать значение 60, если также разрешено использование високосной секунды.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow.<br>startTime.<br>nanos | **integer** (int32)<br><p>Доли секунды (в наносекундах). Допустимые значения: от 0 до 999999999.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>dailyMaintenanceWindow.<br>duration | **string**<br><p>Длительность окна обновлений.</p> <p>Допустимые значения — от 3600 seconds до 86400 seconds включительно.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow | **object**<br>Обновление мастера в выбранные дни в течение указанного временного окна. <br>`clusters[].master.maintenancePolicy.maintenanceWindow` включает только одно из полей `anytime`, `dailyMaintenanceWindow`, `weeklyMaintenanceWindow`<br><br>
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[] | **object**<br><p>Обязательное поле. Дни недели и окно обновлений для этих дней, когда разрешены автоматические обновления.</p> <p>Количество элементов должно находиться в диапазоне от 1 до 7.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>days[] | **string**<br><p>Represents a day of week.</p> <ul> <li>DAY_OF_WEEK_UNSPECIFIED: The unspecified day-of-week.</li> <li>MONDAY: The day-of-week of Monday.</li> <li>TUESDAY: The day-of-week of Tuesday.</li> <li>WEDNESDAY: The day-of-week of Wednesday.</li> <li>THURSDAY: The day-of-week of Thursday.</li> <li>FRIDAY: The day-of-week of Friday.</li> <li>SATURDAY: The day-of-week of Saturday.</li> <li>SUNDAY: The day-of-week of Sunday.</li> </ul> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>startTime | **object**<br><p>Обязательное поле. Время начала окна обновлений, указывается в часовом поясе UTC.</p> <p>Время суток. Дата и часовой пояс либо не учитываются, либо задаются в других местах.</p> <p>API может разрешить использование високосной секунды.</p> <p>Связанные типы: <a href="https://github.com/googleapis/googleapis/blob/master/google/type/date.proto">google.type.Date</a> и <a href="https://github.com/protocolbuffers/protobuf/blob/master/src/google/protobuf/timestamp.proto">google.protobuf.Timestamp</a>.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>startTime.<br>hours | **integer** (int32)<br><p>Часы. Допустимые значения: от 0 до 23.</p> <p>API может разрешить использовать значение в формате &quot;24:00:00&quot; в требующих этого сценариях (например, для указания времени закрытия учреждения).</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>startTime.<br>minutes | **integer** (int32)<br><p>Минуты. Допустимые значения: от 0 до 59.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>startTime.<br>seconds | **integer** (int32)<br><p>Секунды. Стандартные допустимые значения: от 0 до 59.</p> <p>API может разрешить использовать значение 60, если также разрешено использование високосной секунды.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>startTime.<br>nanos | **integer** (int32)<br><p>Доли секунды (в наносекундах). Допустимые значения: от 0 до 999999999.</p> 
clusters[].<br>master.<br>maintenancePolicy.<br>maintenanceWindow.<br>weeklyMaintenanceWindow.<br>daysOfWeek[].<br>duration | **string**<br><p>Длительность окна обновлений.</p> <p>Допустимые значения — от 3600 seconds до 86400 seconds включительно.</p> 
clusters[].<br>master.<br>zonalMaster | **object**<br>Параметры зоны доступности мастера. <br>`clusters[].master` включает только одно из полей `zonalMaster`, `regionalMaster`<br><br>
clusters[].<br>master.<br>zonalMaster.<br>zoneId | **string**<br><p>Идентификатор зоны доступности, в которой находится мастер.</p> 
clusters[].<br>master.<br>zonalMaster.<br>internalV4Address | **string**<br><p>Внутренний IPv4-адрес, назначенный мастеру.</p> 
clusters[].<br>master.<br>zonalMaster.<br>externalV4Address | **string**<br><p>Внешний IPv4-адрес, назначенный мастеру.</p> 
clusters[].<br>master.<br>regionalMaster | **object**<br>Параметры региона для мастера. <br>`clusters[].master` включает только одно из полей `zonalMaster`, `regionalMaster`<br><br>
clusters[].<br>master.<br>regionalMaster.<br>regionId | **string**<br><p>Идентификатор региона, в котором находится мастер.</p> 
clusters[].<br>master.<br>regionalMaster.<br>internalV4Address | **string**<br><p>Внутренний IPv4-адрес, назначенный мастеру.</p> 
clusters[].<br>master.<br>regionalMaster.<br>externalV4Address | **string**<br><p>Внешний IPv4-адрес, назначенный мастеру.</p> 
clusters[].<br>ipAllocationPolicy | **object**<br>Политика распределения IP-адресов для служб и модулей внутри кластера Kubernetes в разных зонах доступности.<br>
clusters[].<br>ipAllocationPolicy.<br>clusterIpv4CidrBlock | **string**<br><p>CIDR. Диапазон IP-адресов для подов.</p> <p>Диапазон не должен пересекаться ни с одной подсетью в облачной сети, в которой находится кластер Kubernetes. Статические маршруты будут настроены для этих блоков CIDR в подсетях узлов.</p> 
clusters[].<br>ipAllocationPolicy.<br>serviceIpv4CidrBlock | **string**<br><p>CIDR. Диапазон IP-адресов для сервисов.</p> <p>Диапазон не должен пересекаться ни с одной подсетью в облачной сети, в которой находится кластер Kubernetes.</p> 
clusters[].<br>serviceAccountId | **string**<br><p>Сервисный аккаунт, используемый для выделения Compute Cloud и VPC ресурсов для кластера Kubernetes.</p> 
clusters[].<br>nodeServiceAccountId | **string**<br><p>Сервисный аккаунт, используемый узлами кластера Kubernetes для доступа к Container Registry или для загрузки логов и метрик узла.</p> 
clusters[].<br>releaseChannel | **string**<br>При создании кластера Kubernetes вы должны указать один из трех релизных каналов. Релизный канал содержит несколько версий Kubernetes. Каналы отличаются набором доступных версий, управлением автоматическими обновлениями и получаемыми обновлениями. Изменить канал после создания кластера Kubernetes нельзя, возможно только пересоздать кластер Kubernetes и указать новый релизный канал. Дополнительные сведения см. в [documentation](https://cloud.yandex.com/docs/managed-kubernetes/concepts/release-channels-and-updates).<br><ul> <li>RAPID: На канале часто появляются минорные обновления, содержащие новую функциональность и улучшения. Вы не можете отключить автоматическое обновление на этом канале, но вы можете указать период времени для автоматического обновления.</li> <li>REGULAR: Новая функциональность и улучшения порциями попадают на канал через некоторое время после того, как были предоставлены на канале ``RAPID``.</li> <li>STABLE: На канале происходят только обновления, касающиеся исправление ошибок или улучшения безопасности.</li> </ul> 
clusters[].<br>networkPolicy | **object**<br>
clusters[].<br>networkPolicy.<br>provider | **string**<br>
clusters[].<br>gatewayIpv4Address | **string**<br><p>Адрес шлюза IPv4.</p> <p>Максимальная длина строки в символах — 15.</p> 
nextPageToken | **string**<br><p>Токен для получения следующей страницы результатов в ответе. Если количество результатов больше чем <a href="/docs/managed-kubernetes/api-ref/Cluster/list#query_params">pageSize</a>, используйте ``next_page_token`` в качестве значения параметра <a href="/docs/managed-kubernetes/api-ref/Cluster/list#query_params">pageToken</a> в следующем запросе списка ресурсов. Все последующие запросы будут получать свои значения ``next_page_token`` для перебора страниц результатов.</p> 