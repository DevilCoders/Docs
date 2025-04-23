# Deploy

### Deploy via systemd

1. Install both packages:
* yandex-kube-apiserver
* yandex-kube-apiserver-conf
2. Generate certificates for auth proxy and api-server api
3. Run systemd units kube-auth-webhook kube-apiserver
