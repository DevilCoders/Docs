# Работа со снапшотами

В {{ managed-k8s-name }} доступны [снапшоты](https://kubernetes.io/docs/concepts/storage/volume-snapshots/) — копии дисков [PersistentVolume](../concepts/volume.md#provisioning-volumes) на определенный момент времени.

Чтобы создать снапшот, а потом восстановить его:
1. [{#T}](#create-pvc-pod).
1. [{#T}](#create-snapshot).
1. [{#T}](#restore-from-snapshot).

## Перед началом работы {#before-you-begin}

1. [Создайте кластер {{ managed-k8s-name }} ](../../managed-kubernetes/operations/kubernetes-cluster/kubernetes-cluster-create.md) и [группу узлов](../../managed-kubernetes/operations/node-group/node-group-create.md) любой подходящей конфигурации с версией {{ k8s }} не ниже 1.20.

1. {% include [Install and configure kubectl](../../_includes/managed-kubernetes/kubectl-install.md) %}

## Подготовьте тестовое окружение {#create-pvc-pod}

Для проверки работы со снапшотами будет создан [PersistentVolumeClaim](../concepts/volume.md#persistent-volume) и [под](../concepts/index.md#pod), имитирующий рабочую нагрузку.
1. Создайте файл `01-pvc.yaml` с манифестом `PersistentVolumeClaim`:

   {% if product == "yandex-cloud" %}

   ```yaml
   ---
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-dynamic
   spec:
     accessModes:
       - ReadWriteOnce
     storageClassName: yc-network-hdd
     resources:
       requests:
         storage: 5Gi
   ```

   {% endif %}

   {% if product == "cloud-il" %}

   ```yaml
   ---
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-dynamic
   spec:
     accessModes:
       - ReadWriteOnce
     storageClassName: yc-network-ssd
     resources:
       requests:
         storage: 5Gi
   ```

   {% endif %}

1. Создайте `PersistentVolumeClaim`:

   ```bash
   kubectl apply -f 01-pvc.yaml
   ```

1. Убедитесь, что `PersistentVolumeClaim` создан и имеет состояние `Pending`:

   ```bash
   kubectl get pvc pvc-dynamic
   ```

1. Создайте файл `02-pod.yaml` с манифестом пода `pod-source`:

   ```yaml
   ---
   apiVersion: v1
   kind: Pod
   metadata:
     name: pod-source
   spec:
     containers:
       - name: app
        image: ubuntu
        command: ["/bin/sh"]
         args:
           ["-c", "while true; do echo $(date -u) >> /data/out.txt; sleep 5; done"]
         volumeMounts:
           - name: persistent-storage
             mountPath: /data
     volumes:
       - name: persistent-storage
         persistentVolumeClaim:
           claimName: pvc-dynamic
   ```

   Контейнер пода будет записывать текущие дату и время в файл `/data/out.txt`.

1. Создайте под `pod-source`:

   ```bash
   kubectl apply -f 02-pod.yaml
   ```

1. Убедитесь, что под перешел в состояние `Running`:

   ```bash
   kubectl get pod pod-source
   ```

1. Убедитесь, что в файл `/data/out.txt` попадают записи даты и времени. Для этого [выполните команду](https://kubernetes.io/docs/tasks/debug-application-cluster/get-shell-running-container/) на поде:

   ```bash
   kubectl exec pod -- tail /data/out.txt
   ```

   Результат:

   ```text
   Thu Feb 3 04:55:21 UTC 2022
   Thu Feb 3 04:55:26 UTC 2022
   ...
   ```

## Создайте снапшот {#create-snapshot}

1. Создайте файл `03-snapshot.yaml` с манифестом [снапшота](https://kubernetes.io/docs/concepts/storage/volume-snapshots/#volumesnapshots):

   ```yaml
   ---
   apiVersion: snapshot.storage.k8s.io/v1beta1
   kind: VolumeSnapshot
   metadata:
     name: new-snapshot-test
   spec:
     volumeSnapshotClassName: yc-csi-snapclass
     source:
       persistentVolumeClaimName: pvc-dynamic
   ```

1. Создайте снапшот:

   ```bash
   kubectl apply -f 03-snapshot.yaml
   ```

1. Убедитесь, что снапшот создан:

   ```bash
   kubectl get volumesnapshots.snapshot.storage.k8s.io
   ```

1. Убедитесь, что создан [VolumeSnapshotContent](https://kubernetes.io/docs/concepts/storage/volume-snapshots/#introduction):

   ```bash
   kubectl get volumesnapshotcontents.snapshot.storage.k8s.io
   ```

## Восстановите объекты из снапшота {#restore-from-snapshot}

При [восстановлении из снапшота](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-snapshot-and-restore-volume-from-snapshot-support) в кластере будут созданы:
* Объект `PersistentVolumeClaim` с именем `pvc-restore`.
* Под с именем `pod-restore`, содержащий записи в файле `/data/out.txt`.

Чтобы восстановить снапшот:
1. Создайте файл `04-restore-snapshot.yaml` с манифестом нового `PersistentVolumeClaim`:

   {% if product == "yandex-cloud" %}

   ```yaml
   ---
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-restore
   spec:
     storageClassName: yc-network-hdd
     dataSource:
       name: new-snapshot-test
       kind: VolumeSnapshot
       apiGroup: snapshot.storage.k8s.io
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 10Gi
   ```

   {% endif %}

   {% if product == "cloud-il" %}

   ```yaml
   ---
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-restore
   spec:
     storageClassName: yc-network-ssd
     dataSource:
       name: new-snapshot-test
       kind: VolumeSnapshot
       apiGroup: snapshot.storage.k8s.io
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 10Gi
   ```

   {% endif %}

   {% note tip %}

   Вы можете изменить размер создаваемого `PersistentVolumeClaim`. Для этого укажите нужный размер в значении настройки `spec.resources.requests.storage`.

   {% endnote %}

1. Создайте новый `PersistentVolumeClaim`:

   ```bash
   kubectl apply -f 04-restore-snapshot.yaml
   ```

1. Убедитесь, что `PersistentVolumeClaim` создан и имеет состояние `Pending`:

   ```bash
   kubectl get pvc pvc-restore
   ```

1. Создайте файл `05-pod-restore.yaml` с манифестом нового пода `pod-restore`:

   ```yaml
   ---
   apiVersion: v1
   kind: Pod
   metadata:
     name: pod-restore
   spec:
     containers:
       - name: app-restore
         image: ubuntu
         command: ["/bin/sh"]
         args: ["-c", "while true; do sleep 5; done"]
         volumeMounts:
           - name: persistent-storage-r
             mountPath: /data
     volumes:
       - name: persistent-storage-r
         persistentVolumeClaim:
           claimName: pvc-restore
   ```

   Контейнер нового пода не будет производить никаких действий с файлом `/data/out.txt`.

1. Создайте под `pod-restore`:

   ```bash
   kubectl apply -f 05-pod-restore.yaml
   ```

1. Убедитесь, что под перешел в состояние `Running`:

   ```bash
   kubectl get pod pod-restore
   ```

1.  Убедитесь, что новый `PersistentVolumeClaim` перешел в состояние `Bound`:

   ```bash
   kubectl get pvc pvc-restore
   ```

1. Убедитесь, что файл `/data/out.txt` на новом поде содержит записи, которые контейнер пода `pod-source` [записал в файл](#create-pvc-pod) до создания снапшота:

   ```bash
   kubectl exec pod-restore -- tail /data/out.txt
   ```

   Результат:

   ```text
   Thu Feb 3 04:55:21 UTC 2022
   Thu Feb 3 04:55:26 UTC 2022
   ...
   ```

## Удалите созданные ресурсы {#clear-out}

Если созданные ресурсы вам больше не нужны, удалите их:
1. [Удалите кластер {{ managed-k8s-name }}](../../managed-kubernetes/operations/kubernetes-cluster/kubernetes-cluster-delete.md).
1. Если вы зарезервировали для кластера публичный статический IP-адрес, [удалите его](../../vpc/operations/address-delete.md).
1. [Удалите снимок диска](../../compute/operations/snapshot-control/delete.md).