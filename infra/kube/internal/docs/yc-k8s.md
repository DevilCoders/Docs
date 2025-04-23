# Outline		
Fully functional control plane needs:		
  * IPv6 connectivity with interal Yandex networks (optional for now)		
  * Internet connectivity (to access cr.yandex and other external resources, like Azure)		
  * Being set up across several AZ (optional for now)		

# Prerequisites		
We need `yc` command line tool to manage Yandex.Cloud resource:		
  *  Install using [official documentation](https://cloud.yandex.ru/docs/cli/operations/install-cli#interactive).		
  * Log in: `yc init --federation-id yc.yandex-team.federation`.		

# Setup network		
Yandex cloud provided documentation: [here](https://wiki.yandex-team.ru/users/nrkk/kubernetes-v-ipv6-setjax/). Create VPC and subnets (TODO). If we need **rtc<->yc** connectivity, we need IPv6. At the moment only way to get dualstack networks - creating ticket like [CLOUD-74046](https://st.yandex-team.ru/CLOUD-74046).		

# Setup credentials		

  * Create service account for k8s [(doc)](https://cloud.yandex.ru/docs/iam/operations/sa/create):		
```shell		
yc iam service-account create --name default		
```		
  * Assign:		
    * `editor` role to sa on folder to allow resource creation needed by k8s		
    * `container-registry.images.puller` role to sa to allow pull images from registry		
```shell		
SA_NAME=default		
FOLDER_NAME=crossplane		
SA_ID=$(yc iam service-account get $SA_NAME --format json | jq -r .id)		
yc resource-manager folder add-access-binding $FOLDER_NAME \		
    --role editor \		
    --subject "serviceAccount:$SA_ID"		
yc resource-manager folder add-access-binding $FOLDER_NAME \		
    --role container-registry.images.puller \		
    --subject "serviceAccount:$SA_ID"		
```		
# Setup managed kubernetes		
Official documentation can be found [here](https://cloud.yandex.ru/docs/managed-kubernetes/operations/kubernetes-cluster/kubernetes-cluster-create).		

<details>		
<summary>Note: regional mode not available.</summary>		
Note: ideally we want regional cluster (for availability), but at the moment this does not work:		

```		
ERROR: rpc error: code = InvalidArgument desc = Validation error:		
master_spec.regional_master_spec.locations[0].internal_v4_address_spec.subnet_id: There is more than one subnet for network "enpvkeqqi7egqcrdrg8u" in zone "ru-central1-a", please specify subnet to use		
ERROR: rpc error: code = InvalidArgument desc = Validation error:		
master_spec.regional_master_spec.locations[0].zone_id: Field is required		
```		

</details>		

Note: cluster nodes will have IPv6 private addresses, but kubernetes master will not		


Setting up:		
  * Create cluster:		
```shell		
yc managed-kubernetes cluster create \		
    --name crossplane \		
    --network-name rtc-to-yc-network \		
    --zone ru-central1-a \		
    --subnet-name rtc-to-yc-network-ru-ru-central1-a \		
    --release-channel rapid \		
    --version 1.19 \		
    --cluster-ipv4-range 10.1.0.0/16 \		
    --service-ipv4-range 10.2.0.0/16 \		
    --service-account-name default \		
    --node-service-account-name default \		
    --daily-maintenance-window start=22:00,duration=10h \		
    --cluster-ipv6-range fc00::/96 \		
    --service-ipv6-range fc01::/112 \		
    --dual-stack		
```		

* Create nodegroup [(doc)](https://cloud.yandex.ru/docs/managed-kubernetes/operations/node-group/node-group-create#node-group-create)		
```shell		
yc managed-kubernetes node-group create \		
  --name crossplane-node-group \		
  --cluster-name crossplane \		
  --platform-id standard-v2 \		
  --cores 2 \		
  --memory 4 \		
  --core-fraction 50 \		
  --disk-type network-ssd \		
  --disk-size 96 \		
  --fixed-size 2 \		
  --version 1.19 \		
  --daily-maintenance-window start=22:00,duration=10h \		
  --network-interface=ipv6-address=auto,ipv4-address=auto,subnets=rtc-to-yc-network-ru-ru-central1-a		
```		

* Login kubectl in yc k8s		
```shell		
yc managed-kubernetes cluster get-credentials --id <cluster-id> --external		
```		

* Create managed docker registry ([doc](https://cloud.yandex.ru/docs/container-registry/quickstart/))		

```shell		
yc container registry create --name provider-azure		
```		

Configure docker client on dev localhost		

```shell		
yc container registry configure-docker		
```		
* Add `docker.config` in external k8s secrets to allow pull images from external registry		

```bash		
# May be you need other token, not from ~/.docker/config.json like in example		
cd ~/.docker		
kubectl --context <external-k8s> create secret generic regcred \		
    --from-file=.dockerconfigjson=config.json \		
    --type=kubernetes.io/dockerconfigjson		
```		

