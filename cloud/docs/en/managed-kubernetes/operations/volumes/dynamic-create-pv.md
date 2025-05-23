# Dynamic volume provisioning

Create a [pod](../../concepts/index.md#pod) with a dynamically provisioned [volume](../../concepts/volume.md):
1. [Create a PersistentVolumeClaim](#create-pvc).
1. [Create a pod](#create-pod).

{% note tip %}

You can use a [bucket](../../../storage/concepts/bucket.md) in {{ objstorage-full-name }} as storage for the pod. For more information, see [{#T}](s3-csi-integration.md).

{% endnote %}

## Create a PersistentVolumeClaim object {#create-pvc}

1. Save the following `PersistentVolumeClaim` creation specification to a YAML file named `pvc-dynamic.yaml`.

   {% if product == "yandex-cloud" %}

   {% note info %}

   If the `storageClassName` parameter is not specified, the default storage class (`yc-network-hdd`) is used. To change the default class, see [{#T}](manage-storage-class.md#sc-default).

   {% endnote %}

   {% endif %}

   For more on specifications for creating `PersistentVolumeClaim` objects, see the [{{ k8s }} documentation](https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/persistent-volume-claim-v1/).

   {% if product == "yandex-cloud" %}

   ```
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
         storage: 4Gi
   ```

   {% endif %}

   {% if product == "cloud-il" %}

   ```
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
         storage: 4Gi
   ```

   {% endif %}

   1. Run the command:

      ```bash
      kubectl create -f pvc-dynamic.yaml
      ```

      Result:

      ```
      persistentvolumeclaim/pvc-dynamic created
      ```

   1. View information about the `PersistentVolumeClaim` created:

      ```bash
      kubectl describe persistentvolumeclaim pvc-dynamic
      ```

      Result:

      {% if product == "yandex-cloud" %}

      ```
      Name:          pvc-dynamic
      Namespace:     default
      StorageClass:  yc-network-hdd
      Status:        Pending
      ...
      Events:
      Type    Reason                Age               From                         Message
      ----    ------                ----              ----                         -------
      Normal  WaitForFirstConsumer  9s (x3 over 15s)  persistentvolume-controller  waiting for first consumer to be created before binding
      ```

      {% endif %}

      {% if product == "cloud-il" %}

      ```
      Name:          pvc-dynamic
      Namespace:     default
      StorageClass:  yc-network-ssd
      Status:        Pending
      ...
      Events:
      Type    Reason                Age               From                         Message
      ----    ------                ----              ----                         -------
      Normal  WaitForFirstConsumer  9s (x3 over 15s)  persistentvolume-controller  waiting for first consumer to be created before binding
      ```

      {% endif %}

## Create a pod with a dynamically provisioned volume {#create-pod}

1. Save the following pod creation specification to a YAML file named `pod.yaml`.

   More information on specifications for creating pods is available in the [{{ k8s }} documentation](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/).

   ```
   apiVersion: v1
   kind: Pod
   metadata:
     name: pod
   spec:
     containers:
     - name: app
       image: ubuntu
       command: ["/bin/sh"]
       args: ["-c", "while true; do echo $(date -u) >> /data/out.txt; sleep 5; done"]
       volumeMounts:
       - name: persistent-storage
         mountPath: /data
     volumes:
     - name: persistent-storage
       persistentVolumeClaim:
         claimName: pvc-dynamic
   ```

1. Run the command:

   ```bash
   kubectl create -f pod.yaml
   ```

   Result:

   ```
   pod/pod created
   ```

1. View information about the pod created:

   ```bash
   kubectl describe pod pod
   ```

   Result:

   ```
   Name:         pod
   Namespace:    default
   Priority:     0
   Node:         cl1gqrct5oier258n08t-ytas/10.0.0.20
   Start Time:   Tue, 23 Jul 2019 19:42:43 +0300
   Labels:       <none>
   Annotations:  <none>
   Status:       Running
   ...
   Events:
     Type    Reason                  Age   From                                Message
     ----    ------                  ----  ----                                -------
     Normal  Scheduled               30s   default-scheduler                   Successfully assigned default/pod to cl1gqrct5oier258n08t-ytas
     Normal  SuccessfulAttachVolume  28s   attachdetach-controller             AttachVolume.Attach succeeded for volume "pvc-c4794058-ad68-11e9-b71a-d00df1cbdf81"
     Normal  Pulling                 21s   kubelet, cl1gqrct5oier258n08t-ytas  pulling image "ubuntu"
     Normal  Pulled                  11s   kubelet, cl1gqrct5oier258n08t-ytas  Successfully pulled image "ubuntu"
     Normal  Created                 10s   kubelet, cl1gqrct5oier258n08t-ytas  Created container
     Normal  Started                 10s   kubelet, cl1gqrct5oier258n08t-ytas  Started container
   ```

   After creating a pod:
   * In the **{{ compute-full-name }}** management console under **Disks**, a new [disk](../../../compute/concepts/disk.md) will appear with the `k8s-csi` prefix in the disk name.
   * You can find disk provisioning information in the `PersistentVolumeClaim` events:

     ```bash
     kubectl describe persistentvolumeclaim pvc-dynamic
     ```

     Result:

     {% if product == "yandex-cloud" %}

     ```
     Name:          pvc-dynamic
     Namespace:     default
     StorageClass:  yc-network-hdd
     Status:        Bound
     Volume:        pvc-c4794058-ad68-11e9-b71a-d00df1cbdf81
     ...
     Events:
       Type    Reason                 Age                    From                                                                                     Message
       ----    ------                 ----                   ----                                                                                     -------
       Normal  WaitForFirstConsumer   4m25s (x5 over 5m1s)   persistentvolume-controller                                                              waiting for first consumer to be created before binding
       Normal  ExternalProvisioning   4m10s (x3 over 4m10s)  persistentvolume-controller                                                              waiting for a volume to be created, either by external provisioner "disk-csi-driver.mks.ycloud.io" or manually created by system administrator
       Normal  Provisioning           4m10s                  disk-csi-driver.mks.ycloud.io_cat1h5l0v862oq74cp8j_d0f0b837-a875-11e9-b6cb-d00df1cbdf81  External provisioner is provisioning volume for claim "default/pvc-dynamic"
       Normal  ProvisioningSucceeded  4m7s                   disk-csi-driver.mks.ycloud.io_cat1h5l0v862oq74cp8j_d0f0b837-a875-11e9-b6cb-d00df1cbdf81  Successfully provisioned volume pvc-c4794058-ad68-11e9-b71a-d00df1cbdf81
     ```

     {% endif %}

     {% if product == "cloud-il" %}

     ```
     Name:          pvc-dynamic
     Namespace:     default
     StorageClass:  yc-network-ssd
     Status:        Bound
     Volume:        pvc-c4794058-ad68-11e9-b71a-d00df1cbdf81
     ...
     Events:
       Type    Reason                 Age                    From                                                                                     Message
       ----    ------                 ----                   ----                                                                                     -------
       Normal  WaitForFirstConsumer   4m25s (x5 over 5m1s)   persistentvolume-controller                                                              waiting for first consumer to be created before binding
       Normal  ExternalProvisioning   4m10s (x3 over 4m10s)  persistentvolume-controller                                                              waiting for a volume to be created, either by external provisioner "disk-csi-driver.mks.ycloud.io" or manually created by system administrator
       Normal  Provisioning           4m10s                  disk-csi-driver.mks.ycloud.io_cat1h5l0v862oq74cp8j_d0f0b837-a875-11e9-b6cb-d00df1cbdf81  External provisioner is provisioning volume for claim "default/pvc-dynamic"
       Normal  ProvisioningSucceeded  4m7s                   disk-csi-driver.mks.ycloud.io_cat1h5l0v862oq74cp8j_d0f0b837-a875-11e9-b6cb-d00df1cbdf81  Successfully provisioned volume pvc-c4794058-ad68-11e9-b71a-d00df1cbdf81
     ```

     {% endif %}