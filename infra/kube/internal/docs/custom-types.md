# Custom types
Нам нужны будут собственные типы данных с собственной схемой:
>Я как разработчик инфраструктуры хочу предоставить DNSRecord'ы AWACS'а в виде объектов KRM (Kubernetes Resource Model).


У kubernetes есть два механизма расширения:
  * custom api server ([1](https://github.com/kubernetes/apiserver), [2](https://github.com/kubernetes/sample-apiserver), [3](https://github.com/kubernetes-sigs/apiserver-builder-alpha))
  позволяет использовать protobuf, отказаться от встроенных resource'ов и нужные нам механимзы аутентификации
  * custom resource definitions - [CRD](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
  позволяет использовать штатный kube-apiserver

Мы выделили небольшой time slice для исследования сборки кастомного api server'а и не добились успехов. Текущая гипотеза:
  * использовать CRD
  * генерировать их с помощью Go IDL, принятому в k8s

# Python client
Есть готовый (автогенерируемый) [клиент для Python](https://github.com/kubernetes-client/python):
  * развивается и поддерживается
  * нетипизированный (все объекты - dict'ы)
  * реализована поддержка leaderelection

# Go client.
Основной и самый развитой клиент - [kubernetes/client-go](https://github.com/kubernetes/client-go/). Для работы требует кодогенерированные структуры, реализующие определённый интерфейс. К сожалению, кодогенерация достаточно сложно отчуждается пока. Дальше всех в исследовании зашёл [Женя Чекалов](https://staff.yandex-team.ru/reddi). От него сырой рецепт:
```bash
mkdir -p /tmp/ggg; cd /tmp/ggg
git clone https://github.com/kubernetes/code-generator
cd code-generator; git checkout v0.20.0
go mod edit -require a.yandex-team.ru/junk/reddi/allocation-ctl@v0.0.0-local -replace=a.yandex-team.ru/junk/reddi/allocation-ctl=`realpath --relative-to=. $ARCADIA_ROOT`/junk/reddi/allocation-ctl
cat > $ARCADIA_ROOT/junk/reddi/allocation-ctl/go.mod <<EOF
module a.yandex-team.ru/allocation-ctl

go 1.16

require k8s.io/apimachinery v0.20.0
EOF
go mod download k8s.io/apimachinery@v0.20.0
./generate-groups.sh all a.yandex-team.ru/junk/reddi/allocation-ctl/pkg/generated a.yandex-team.ru/junk/reddi/allocation-ctl/pkg/apis allocationctl:v1alpha1 --go-header-file ./hack/boilerplate.go.txt  --output-base /tmp/generated/
rm $ARCADIA_ROOT/junk/reddi/allocation-ctl/go.mod
cp /tmp/generated/a.yandex-team.ru/junk/reddi/allocation-ctl/pkg/apis/allocationctl/v1alpha1/zz_generated.deepcopy.go $ARCADIA_ROOT/junk/reddi/allocation-ctl/pkg/apis/allocationctl/v1alpha1/
cp -R /tmp/generated/a.yandex-team.ru/junk/reddi/allocation-ctl/pkg/generated $ARCADIA_ROOT/junk/reddi/allocation-ctl/pkg
TMP_DIR=`mktemp -d`
cd $TMP_DIR
go mod init tmp
GOBIN=/tmp/ggg go get sigs.k8s.io/controller-tools/cmd/controller-gen@v0.4.1
cd $ARCADIA_ROOT/junk/reddi/allocation-ctl
rm -rf $TMP_DIR
mkdir manifests
/tmp/ggg/controller-gen crd paths="./pkg/..." output:crd:artifacts:config=./manifests

```

# Possible future
Текущий план (хотя и с непонятным статусом) описан в [KEP 2309: An IDL for Kubernetes](https://github.com/kubernetes/enhancements/pull/2310). Краткое описание (хотя лучше почитать полную версию):
  * появится **[новый IDL](https://github.com/DirectXMan12/idl/)**
  * первый генератор будет уметь в types.gо c текущей схемой аннотаций в комментариях
КДПВ:
```

/// core/v1 describes core k8s concepts
group-version(group:"core", version:"v1") {
    /// Pod is a group of related, colocated processes
    ///
    /// # Example
    /// apiVersion: v1
    /// kind: Pod
    /// spec: { ... }
    kind Pod {
        // types may be nested -- this is just a convininence for namespacing
        // it does not imply privacy or anything

        spec: Spec,
        struct Spec {
            // list-maps are ordered maps whose keys appear in their body.
            // not specifying a key defaults to `key: name`.
            // Go represets them as lists with specific merge keys, other
            // languages may represent them other ways.
            // They are automatically merged as maps in SMD.

            // optional fields must list the keyword `optional` before the
            // type.

            /// list of volumes that can be mounted by containers belonging to
            /// the pod
            volumes: optional list-map(value: Volume),

            // ...

            dnsPolicy: optional(default: ClusterFirst) DNSPolicy,

            // simple-maps are unordered maps from string-type values to
            // primitive values
            nodeSelector: optional simple-map(value: string),

            // ...

            @deprecated(msg: "use serviceAccountName instead")
            serviceAccount: optional string,

            // ...

            readinessGates: optional list(value: ReadinessGate),
            struct ReadinessGate { }

            // create-only fields are immutable after creation (see immutability KEP)
            containers: create-only list-map(value: Container),
            struct Container {
                name: string,
                // ...
            }
        }

        status: Status,

        struct Status {

        }
    }

    newtype DNSLabel: string validates(pattern: "[a-z0-9]([-a-z0-9]*[a-z0-9])?", max-length: 64);

```
