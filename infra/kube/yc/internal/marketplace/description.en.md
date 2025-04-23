# Crossplane 1.6.1 with Yandex Cloud support

[Crossplane](https://crossplane.io) is an open source Kubernetes add-on that enables platform teams to assemble
infrastructure from multiple vendors, and expose higher level self-service APIs for application teams to consume.

**How to deploy**

1. Open [management console](https://console.cloud.yandex.ru/) and select the Kubernetes cluster.
2. Go to the **Marketplace** tab.
3. Choose **Crossplane**.
4. Click **Use**.
5. Press **Install**.
6. Create a service account [in management console](https://cloud.yandex.com/en/docs/iam/operations/sa/create), or with
   CLI command:

```
yc iam service-account create --name crossplane --folder-id <FOLDER_ID>
```

7. Assign the role of `admin` to the service
   account [in Web console](https://cloud.yandex.com/en/docs/iam/operations/sa/assign-role-for-sa) or with CLI command:

```
yc resource-manager folder add-access-binding <FOLDER_ID> --role admin --subject serviceAccount:<SERVICE_ACCOUNT_ID>
```

8. Create authorized service account key and copy the resulting output with the following command:

```
yc iam key create --service-account-id <SERVICE_ACCOUNT_ID> --output sa-key.json && tr -d '\n' < sa-key.json
```

9. Create kubernetes secret with service account key:

```
kubectl create secret generic yc-creds -n "crossplane-system" --from-file=credentials=./sa-key.json
```

10. Apply ProviderConfig:

```
kubectl apply -f https://raw.githubusercontent.com/yandex-cloud/provider-jet-yc/main/examples/providerconfig/providerconfig.yaml
```

## Use cases

* Cloud resources management via Kubernetes.
* Multi-cloud intrastructure management.

## Useful links

[Documentation](https://crossplane.io/docs/)<br/>

## Technical support

Yandex.Cloud technical support is available to respond to requests 24 hours a day, 7 days a week. The types of requests
handled and the relevant response times depend on your pricing plan. You can activate paid support in
the [management console](https://console.cloud.yandex.com/support?section=plan). Learn more about
requesting [technical support](https://cloud.yandex.com/docs/support/overview).

## License agreement

By using this product you agree to
the [Yandex Cloud Marketplace Terms of Service](https://yandex.com/legal/cloud_terms_marketplace/) and the terms and
conditions of the following
software: [Crossplane provider-jet-yc](https://github.com/yandex-cloud/provider-jet-yc/blob/main/LICENSE)
, [Crossplane](https://github.com/crossplane/crossplane/blob/master/LICENSE).

