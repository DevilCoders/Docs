## Tableau

### Tableau Refresh

#### Preset: [projects/vertis-dwh/tableau-refresh](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/presets/projects/vertis-dwh/tableau-refresh.jinja)
Запуск экстракта сущности Tableau через REST API. Триггером задается CRON-выражение или список артефактов обновленных с одинаковым пользовательским временем (*Updated with same timestamp* в Реакторе)

##### Параметры
| Название | Обязательный | Описание | Возможные значения |
|---|---|---|---|
| `reaction_path` | <ul><li>- [x] </li></ul> | Путь до реакции в Реакторе. По аналогичному пути автоматически будет добавлен артефакт, который публикуется после успешного запуска рефреша | |
| `tableau_resource_type` | <ul><li>- [x] </li></ul> | Тип сущности Tableau | `Workbook`, `Datasource`, `Schedule`
| `tableau_resource_name` | <ul><li>- [x] </li></ul> | Название сущности в Tableau | |
| `artifact_refs` | <ul><li>- [ ] </li></ul> | Список артефактов для триггера. Задается либо список артефактов либо `cron_expression`. **Один из этих параметров нужно задать обязательно!** | |
| `cron_expression` | <ul><li>- [ ] </li></ul> | CRON-выражение для триггера (игнорируется если задан `artifact_refs`) | [CRON builder](https://www.freeformatter.com/cron-expression-generator-quartz.html) |
| `delay_alert_hours` | <ul><li>- [ ] </li></ul> | Добавить алерт на задержку публикации артефакта, который сработает, если артефакт не был опубликован до `delay_alert_hours` часов дня | 0-24 |

##### Примеры
###### Триггер по списку артефактов
```yaml
preset: projects/vertis-dwh/tableau-refresh
preset_options:
  reaction_path: /verticals/vertis-bi/tableau/auto/revenue/r_tableau_auto_revenue_refresh
  tableau_resource_type: "Schedule"
  tableau_resource_name: "Auto revenue new"
  artifact_refs:
  - /verticals/vertis-bi/dm/pg/auto/client/a_pg_dm_auto_manager_uid_d_h_1d
  - /verticals/vertis-bi/dm/pg/auto/revenue/a_pg_dm_auto_revenue_a_1d
  delay_alert_hours: 7
```
###### Триггер по CRON
```yaml
preset: projects/vertis-dwh/tableau-refresh
preset_options:
  reaction_path: /verticals/vertis-bi/tableau/realty/offer/r_realty_offer_a_day_tableau_refresh
  tableau_resource_type: "Schedule"
  tableau_resource_name: "Realty Daily Refresh"
  cron_expression: 0 0 6 * * ?
```
