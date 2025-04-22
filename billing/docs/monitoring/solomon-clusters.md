# Кластеры Solomon
При обновлении списка и содержания манифестов список кластеров в Solomon обновится соответствующим образом. Найти его можно [тут](https://monitoring.yandex-team.ru/projects/newbilling-tarification/clusters/newbilling-tarification_faas-prod/host-groups/view).

## Входные параметры команды

`--env`: **Окружение, в котором обновляется список кластеров**. `prod`, `dev` или `test`.

`--dc_names`: **Список датацентров**. Для каждого ДЦ из этого списка создается кластер для каждого из сервисов/тенантов. Разделитель - запятая, пример: `--dc_names=vla,sas`.
