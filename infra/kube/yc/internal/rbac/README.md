# Setup RBAC for ASO in Crossplane cluster

NOTE: Right now there is no way to grant access via username or email. And we use iam user id. More
in [CLOUDSUPPORT-88172](https://st.yandex-team.ru/CLOUDSUPPORT-88172)

## Step by step

1. User must have at least resource-manager role

Request DevOps role in [Crossplane RTC](https://abc.yandex-team.ru/services/crossplane_rtc/). Or setup sync on new ABC
service, example [YCLOUD-4200](https://st.yandex-team.ru/YCLOUD-4200)

2. Find user id in [IAM UI section](https://console.cloud.yandex.ru/iam?section=users)

3. Create new kubernetes config file in [infra/kube/yc/internal/rbac](.) by [example.yaml](example.yaml)

4. Apply configurations

```shell
# Check diff
kubectl --context yc-crossplane diff -f infra/kube/yc/internal/rbac
# Apply changes
kubectl --context yc-crossplane apply -f infra/kube/yc/internal/rbac
```
