# Infractl betas

### Build and deploy (don't forget to change username in i.yaml):
```
cd betas/example
ya tool infractl make
ya tool infractl build infra.runtime.bromigo-infractl-beta.yaml
ya tool infractl put infra.runtime.bromigo-infractl-beta.yaml
```

### Configure context

Download admin.pem and admin-key.pem from secret https://yav.yandex-team.ru/secret/sec-01f8fhw9frm1n1ybhfpb3dc0wv/explore/versions
```
wget https://crls.yandex.net/allCAs.pem

kubectl config set-cluster dev-bromigo --certificate-authority ./allCAs.pem --embed-certs --server https://meryhlss7k6sfzko.myt.yp-c.yandex.net/
kubectl config set-credentials admin \
    --client-certificate=admin.pem \
    --client-key=admin-key.pem
kubectl config set-context dev-bromigo --cluster dev-bromigo --user admin
kubectl config use-context dev-bromigo
```
Check connection to api server:
```
kubectl get namespaces
NAME              STATUS   AGE
default           Active   6m36s
kube-node-lease   Active   6m40s
kube-public       Active   6m41s
kube-system       Active   6m41s
```

### Configure cluster:
```
{ kubectl get clusterrolebinding cluster-admin -o yaml; echo "- apiGroup: rbac.authorization.k8s.io\n  kind: User\n  name: robot-infractl"; } | kubectl replace -f -

ya make --add-result .crd.yaml --add-result .go --replace-result \
	controllers/deploy/api/project/proto_v1 \
	controllers/deploy/api/stage/proto_v1 \
	controllers/runtime/api/proto_v1 \
	controllers/roles/api/proto_v1 \
	controllers/awacs/api/upstream/proto_v1 \
	controllers/awacs/api/backend/proto_v1

kubectl create -f controllers/roles/api/proto_v1/rolesconfiguration_types.crd.yaml
kubectl create -f controllers/awacs/api/backend/proto_v1/awacsbackend_types.crd.yaml
kubectl create -f controllers/awacs/api/upstream/proto_v1/awacsupstream_types.crd.yaml
kubectl create -f controllers/deploy/api/project/proto_v1/deployproject_types.crd.yaml
kubectl create -f controllers/deploy/api/stage/proto_v1/deploystage_types.crd.yaml
kubectl create -f controllers/runtime/api/proto_v1/runtime_types.crd.yaml
```
