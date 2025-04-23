# ML Storage Binary Client Library

Библиотека оборачивающая бинарь клиента.

## Использование

### Вызов из бинаря

```py
from sandbox.projects.ads.emily.storage.client.binary import MlStorageBinaryClient, get_arcadia_cli_path
ml_storage = MlStorageBinaryClient(token=os.getenv("ML_STORAGE_TOKEN"))
```

```bash
# Собрать локальный клиент
$ ya make ads/emily/storage/models/client/bin
```

### Для тестов

```py
from logos.libs.clients.sandbox import local_sandbox
from sandbox.projects.ads.emily.storage.client.binary import MlStorageBinaryClient

token = os.getenv("ML_STORAGE_TOKEN")

sb_client = local_sandbox.SandboxClient(token=token)

ml_storage = MlStorageBinaryClient(token, sb_client=sb_client)
```
