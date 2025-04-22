# Полокационная выкладка с ручным подтверждением

Полокационная выкладка нужна тем, кому требуется выкатывать DeployUnit's последовательно в определенном порядке на каждую из локаций, текущая реализация так же позволяет использовать ручные подтверждения при необходимости. Полокационная выкладка работает только для приложений, которые используют **per cluster replica set**.

В случаях, если контроллер управления кластером отличен от **per cluster replica set**, будет ошибка:
```
Deploy settings support only for per cluster type. Deploy unit: $DEPLOY_UNIT_NAME
```

## Как использовать полокационную выкладку {#usage}

Для того, чтобы воспользоваться полокационной выкладкой, необходимо через **dctl** пропатчить спеку, добавив спеку DeployUnit настройки прокластерной выкладки в параметр **deploy_settings**. Наличие этого параметра включает функционал. Схему и тип данных можно посмотреть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=7615865#L214). Порядок локаций, указанный в параметре **cluster_sequence**, будет соответсвовать порядку выкладки. Параметр **need_approval** указывает на то, что для выкладки этой локации необходимо подтверждение. Названия локаций должны соответствовать локациям в настройках **replica_set**. Отсутствие какой-либо локации в **cluster_sequence** говорит о том, что остальные локации едут в произвольном порядке и без подтверждения после тех, для которых порядок указан.

**Пример 1:**

```yaml
spec:
...
  deploy_units:
    deployUnit:
      deploy_settings:
        cluster_sequence:
        - yp_cluster: man
          need_approval: false
        - yp_cluster: sas
          need_approval: true
...
      replica_set:
       per_cluster_settings:
          sas:
            deployment_strategy:
              max_unavailable: 1
            pod_count: 1
        per_cluster_settings:
          man:
            deployment_strategy:
              max_unavailable: 1
            pod_count: 1
...
```

Особенности использования **deployment_strategy** при полокационной выкладке. Параметр **max_unavailable** говорит о том, какое количество подов может быть недоступным в момент выкладки на одну локацию. В случае полокационной выкладки, если **max_unavailable** < **pod_count**, то есть выкладка идет без даунтайма в данной локации, и отсутствует ручное подтверждение, выкладка в следующую локацию начнется как только, количество подов с целевой ревизией в катящейся локации достигнет  **pod_count** - **max_unavailable**. Текущее поведение, при необходимости 100% выкладки локации, решить после появления done_threshold ([https://st.yandex-team.ru/DEPLOY-3640](https://st.yandex-team.ru/DEPLOY-3640))

## Аппрувы {#approves}

Для аппрувов или дисапрувов можно воспользоваться консольным клиентом **dctl**

**Параметры:**
* **--deploy-revision** — ревизия деплой юнита, для которого необходим аппрув, можно получить из спеки по пути <[/spec/deploy_units/[DU_NAME]/revision]>
* **--deploy-unit-id** — имя деплой юнита
* **--clusters** — имя локации (sas, man, vla, ...), можно указать сразу несколько локаций.

**Пример использования:**

```bash
dctl control stage approve crastin-stage --deploy-revision 19 --deploy-unit-id deployUnit --clusters sas --clusters man
```

## Настройка в UI {#ui}

На странице деплой юнита можно отметить использование полокационной выкладки и задать порядок кластеров.
Для любого из кластеров можно отметить обязательное использование апрувов.
![Data.ef74454.png](https://jing.yandex-team.ru/files/nikolaichev/Data.ef74454.png)

После обновления стейджа на странице статуса в случае необходимости апрувов появятся соответствующие кнопки. Также будет указан порядок выкладки.
![Data.9d1be3f.png](https://jing.yandex-team.ru/files/nikolaichev/Data.9d1be3f.png)

После апрува в модальном окне
![Screen%20Shot%202021-02-25%20at%2018.11.42.9e4168f.png](https://jing.yandex-team.ru/files/nikolaichev/Screen%20Shot%202021-02-25%20at%2018.11.42.9e4168f.png)

Появится запись об апруве и соответствующий кластер начнет катится. Необязательно дожидаться, пока он раскатится, можно апрувить остальные.
![Data.48adb8b.png](https://jing.yandex-team.ru/files/nikolaichev/Data.48adb8b.png)

В списке деплой юнитов дополнительно указывается, к которым из них нужны апрувы
![Data.e9a7ec4.png](https://jing.yandex-team.ru/files/nikolaichev/Data.e9a7ec4.png)

