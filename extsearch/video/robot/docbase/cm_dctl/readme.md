# Cluster-Master Deploy CTL
Утилита для обновления динамических ресурсов в системе Deploy.

Позволяет проверить доехал ли ресурс до подов.

Обертка над утилитой dctl (https://deploy.yandex-team.ru/docs/tools/dctl)

## Использование
Необходим токен для доступа к YP (https://deploy.yandex-team.ru/docs/tools/dctl#token)
* Можно передавать через переменную окружения: DCTL_YP_TOKEN
* Можно передавать путь к токену через `--yp_token`

## Пример команд

### Обновить динамический ресурс
```shell
./cm_dctl update_dr --yp_token ~/.dctl/token --dr_id cluster-master.video-index.VIDEO_ROBOT_CM_VIDEO_BUNDLE_DOCBAS --resource_id 'sbr:2154520928' --dr_dg_mark 'all'
```
Пример ответа:
```json
{
  "stage_revision": 32,
  "dynamic_resource_revision": 3
}
```

### Проверить готовности ревизии динамического ресурса
```shell
./cm_dctl check_dr_revision --yp_cluster vla --yp_token ~/.dctl/token --dr_id cluster-master.video-index.VIDEO_ROBOT_CM_VIDEO_BUNDLE_DOCBAS --revision 3 --number_ready_pods 1
```
Пример ответа NOT_READY:
```
NOT_READY
```
Пример ответа READY:
```
READY
```

### Проверить состояние динамического ресурса
```shell
./cm_dctl state_dr --yp_cluster vla --yp_token ~/.dctl/token --dr_id cluster-master.video-index.VIDEO_ROBOT_CM_VIDEO_BUNDLE_DOCBAS
```
Пример ответа IN_PROGRESS:
```json
{"revision": 3, "ready": 0, "in_progress": 1, "error": 0}
```
Пример ответа READY:
```json
{"revision": 3, "ready": 1, "in_progress": 0, "error": 0}
```

### Получить описание динамического ресурса
```shell
./cm_dctl get_dr --yp_cluster vla --yp_token ~/.dctl/token --dr_id cluster-master.video-index.VIDEO_ROBOT_CM_VIDEO_BUNDLE_DOCBAS
```
