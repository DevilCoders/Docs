# allocation-ctl

```sh

cd $ARCADIA_ROOT/yt/yt/orm/go/orm/discovery/drpc
ya make --add-result .go --replace-result
cd $ARCADIA_ROOT/yp/go/proto/ypapi
ya make --add-result .go --replace-result

mkdir -p /tmp/ggg; cd /tmp/ggg
git clone https://github.com/kubernetes/code-generator
cd code-generator; git checkout v0.20.0
go mod edit -require a.yandex-team.ru/infra/allocation-ctl@v0.0.0-local -replace=a.yandex-team.ru/infra/allocation-ctl=`realpath --relative-to=. $ARCADIA_ROOT`/infra/allocation-ctl
cat > $ARCADIA_ROOT/infra/allocation-ctl/go.mod <<EOF
module a.yandex-team.ru/allocation-ctl

go 1.16

require k8s.io/apimachinery v0.20.0
EOF
go mod download k8s.io/apimachinery@v0.20.0
./generate-groups.sh all a.yandex-team.ru/infra/allocation-ctl/pkg/generated a.yandex-team.ru/infra/allocation-ctl/pkg/apis allocationctl:v1alpha1 --go-header-file ./hack/boilerplate.go.txt  --output-base /tmp/generated/
rm $ARCADIA_ROOT/infra/allocation-ctl/go.mod
cp /tmp/generated/a.yandex-team.ru/infra/allocation-ctl/pkg/apis/allocationctl/v1alpha1/zz_generated.deepcopy.go $ARCADIA_ROOT/infra/allocation-ctl/pkg/apis/allocationctl/v1alpha1/
cp -R /tmp/generated/a.yandex-team.ru/infra/allocation-ctl/pkg/generated $ARCADIA_ROOT/infra/allocation-ctl/pkg
TMP_DIR=`mktemp -d`
cd $TMP_DIR
go mod init tmp
GOBIN=/tmp/ggg go get sigs.k8s.io/controller-tools/cmd/controller-gen@v0.4.1
cd $ARCADIA_ROOT/infra/allocation-ctl
rm -rf $TMP_DIR
mkdir manifests
/tmp/ggg/controller-gen crd paths="./pkg/..." output:crd:artifacts:config=./manifests
```
