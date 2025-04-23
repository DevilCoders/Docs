# Скрипты

## transformScheduleTypesOebsAlias.ts
**Зачем**
Переименовать все значения графиков oebs из формата '*[ чЧ]' на '*Ч' в названии oebs 
TEWFM-935

**Запуск**

Из корня wfm:
```shell
CSRF_TOKEN='<from browser>' COOKIE='<from browser>' ts-node server/utils/scripts/transformScheduleTypesOebsAlias.ts
```
