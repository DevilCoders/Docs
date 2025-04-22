## Права и за что отвечают

| Пермишн фронта       | Значение                                           | Права на беке
-----------------------|----------------------------------------------------|---------------------------------------------------
| can_view             | видеть [use GET], включая базовую информацию о сервисе - название, id, slug, readonlystate     | own_only_viewer OR services_viewer OR full_access
| view_description     | видеть описание сервиса                            | own_only_viewer OR services_viewer OR full_access
| view_own_services    | видеть собственные сервисы                         | own_only_viewer OR services_viewer OR full_access
| view_team            | видеть состав команды сервисов                     | own_only_viewer OR services_viewer OR full_access
| can_filter_and_click | фильтровать и смотреть сервисы (view_all_services) | services_viewer OR full_access
| view_all_services    | видеть все сервисы                                 | services_viewer OR full_access
| view_duty            | видеть дежурства                                   | services_viewer OR full_access
| view_hierarchy       | видеть иерархию сервисов                           | services_viewer OR full_access
| can_edit             | редактировать [use POST/PUT/PATCH/DELETE]          | full_access
| can_export           | экспортировать                                     | full_access
| view_activity        | видеть деятельность сервиса                        | full_access
| view_contacts        | видеть контакты сервиса                            | full_access
| view_department      | видеть подразделение сервиса                       | full_access
| view_details         | видеть детальное описание                          | full_access
| view_hardware        | видеть железо                                      | full_access
| view_kpi             | видеть KPI                                         | full_access
| view_resources       | видеть ресурсы                                     | full_access
| view_tags            | видеть тэги                                        | full_access
| view_traffic_light   | видеть светофор                                    | full_access

## Ручка

Описание ручки в [задаче ABC-8129](https://st.yandex-team.ru/ABC-8129)

Ручка дергается express приложением, в миддлваре [ask-abc-permissions](../../src/express/middlewares/ask-abc-permissions.js), 
результат кладётся в поле `res.locals.permissions`.

Прокидывается в контекст бэм шаблонов миддлварью [abc-controller-html](../../src/express/middlewares/abc-controller-html.js).
