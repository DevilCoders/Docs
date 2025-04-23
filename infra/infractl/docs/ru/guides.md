# Инструкции

## Конвертация спеки стейджа dctl в infractl {#dctl-to-infractl}

* `stage_yaml` - путь до файла с описанием стейджа, полученного командой `dctl get stage my-stage -c xdc > /path/to/stage.yaml`
* `namespace` - имя неймспейса в K8S

```python
import yaml
import yt_yson_bindings
import yt.yson as yson
from google.protobuf import json_format
from yp_proto.yp.client.api.proto import autogen_pb2

stage_yaml = "/path/to/stage.yaml"
namespace = "my-k8s-namespace"

with open(stage_yaml, "r") as f:
    stage_yson = yson.dumps(yaml.safe_load(f))
    pb = yt_yson_bindings.loads_proto(stage_yson, autogen_pb2.TStage)
    d = json_format.MessageToDict(pb)
    r = {
        "apiVersion": "k.yandex-team.ru/v1",
        "kind": "DeployStage",
        "metadata": {
            "name": d["meta"]["id"],
            "namespace": namespace,
        },
        "spec": {
            "stage_spec": d["spec"],
        },
    }
    print(yaml.safe_dump(r))
```

## Кастомные CRD в k8s infractl {#custom-crd}
### Правила именования {#cutom-crd-naming}
API-группу для кастомных CRD (поле `group` в спеке CRD) лучше именовать по такому шаблону: `<group-name>.yandex-team.ru`.
А имя самого CRD (поле `name` в метадате CRD) так: `<resource-name>.<group-name>.yandex-team.ru`.

### Создание кастомных CRD {#cutom-crd-creation}
1. Для `k.yandex-team.ru` необходимо запросить доступ в IDM, как это описано [здесь](https://docs.yandex-team.ru/infractl/howto#access).
2. Если необходимо, заказываем дырку в Панчере до `k.yandex-team.ru`.  `Назначение`: `k.yandex-team.ru`, `Протокол: порты`: `tcp: 443`. Для `k.yandex-team.ru` уже есть [дырка](https://puncher.yandex-team.ru/?id=623b1ae55053cea81d7ff75c) для `@allstaff@`.
3. Просим кого-то из [разработчиков infractl](https://abc.yandex-team.ru/services/infractl/?scope=development) создать необходимые CRD и выдать роль на их редатирование/обновление. В разботчиков необходимо принести:
* yaml-файлы с описанием CRD
* ABC-группу, для которой необходимо дать доступ на редактирование/удаление CRD
