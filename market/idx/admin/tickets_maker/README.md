## Создание тикетов дежурств по расписанию
Тулза котоая умеет создавать тикеты 
1. для дежурств индексатора: https://st.yandex-team.ru/issues/58004
2. для еженедельных статусов: https://st.yandex-team.ru/issues/408412

### Регулярный запуск
Тулза запускается в Sandbox каждый понедельник в 8 утра
https://sandbox.yandex-team.ru/scheduler/44882/view

### Секреты
Для создания тикета используется [токен](https://yav.yandex-team.ru/secret/sec-01dns90xhrhhwat2fvbyw0vv6b) робота [robot-mrkt-idx-sb](https://staff.yandex-team.ru/robot-mrkt-idx-sb)
Соотвеcтвенно тикет создаются от его имени.

Для удобства запуска в Sandbox этот токен продублирован в [Sandbox vault](https://sandbox.yandex-team.ru/admin/vault?owner=razmser&name=robot-mrkt-idx-sb-st-token&limit=20) это можно будет оторвать после того как YA_EXEC научится поддреживать yav

### TVM
TVM id 2032836
[Ресурс в abc](https://abc.yandex-team.ru/services/marketindexer/resources/?search=tickets_maker&view=consuming&layout=cards&show-resource=40482227)
[Токен в yav](https://yav.yandex-team.ru/secret/sec-01fsyxdtsy3acmzt81whjkazdx)
