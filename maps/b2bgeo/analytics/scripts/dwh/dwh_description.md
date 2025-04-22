## Объекты в DataLens

### Подключение
`b2bgeo/connections/b2bgeo_dwh_connection`
https://datalens.yandex-team.ru/connections/noj636u4y0ywi-b2bgeo-dwh-connection

### Примеры датасетов:
`b2bgeo/managers_dashboard/dwh_insights/pipedrive_deals_general`
https://datalens.yandex-team.ru/datasets/jczvcshy4alge-pipedrive-deals-general

### Примеры чартов
`b2bgeo/managers_dashboard/dwh_insights/won_money_wo_renewal`
https://datalens.yandex-team.ru/wizard/zs51oe1vu1j8u-won-money-wo-renewal

### Заезд в Такси DMP:
https://wiki.yandex-team.ru/b2bgeo/analytics/dmp-taxi/

### Плохо структурированный план работ и немного про админство:
https://wiki.yandex-team.ru/users/dante/dwh-architecture-and-postgresql-admin-stuff/

## Материалы с зум-встречи
- видео https://jing.yandex-team.ru/files/dante/DWH_and_DataLens.mp4
- слайды https://jing.yandex-team.ru/files/dante/DataLens_n_sql.pptx

## Technical info
- немного про админство постгреса: https://wiki.yandex-team.ru/b2bgeo/dev/postgresql/
- шпаргалка https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546
- советы про лок-таймауты https://itnan.ru/post.php?c=1&p=452986


# Таблицы в DWH
Какие данные вообще есть?
- Из пайпдрайва - практически все данные есть: сделки, пайплайны и стейджи в пайплайнах, активности по сделкам, организации.
- Также есть таблицы с менеджерами продаж и их месячными/квартальными планами.
- Из mvrp - task_info решенных задач (информация о задаче, без json-реквеста и json-ответа) + предрасчитанная статистика по mvrp/svrp задачам
- Из мониторинга - компании, маршруты, заказы, курьеры + предрасчитанная статистика маршрутов в мониторинге. Нет координат курьеров.
- Из саппорта - тикеты в самсаре.
- Также имеются всевозможные таблицы для проклейки идентификаторов.

## Pipedrive
### pipedrive_deals b2bgeo.pipedrive.com.
Сделки из пайпдрайва. Таблица содержит поля, которые заводятся внутри пайпдрайва, и не содержит те поля, которые мы туда заносим 'снаружи'

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
active | boolean |
activities_count | integer |
add_time | timestamp without time zone |
close_time | timestamp without time zone |
currency | text |
deleted | boolean | практически ни у кого не стоит, кажется
done_activities_count | integer |
email_messages_count | integer |
expected_close_date | date |
last_activity_date | date |
lost_reason | text |
lost_time | timestamp without time zone |
next_activity_date | date |
next_activity_id | integer |
pipeline_id | integer |
probability | real |
rotten_time | timestamp without time zone |
source | text |
stage_change_time | timestamp without time zone |
stage_id | integer |
stage_order_nr | integer |
status | text |
title | text |
undone_activities_count | integer |
update_time | timestamp without time zone |
utm_campaign | text |
utm_medium | text |
utm_source | text |
utm_term | text |
value | real |
vehicles_count | integer |
weighted_value | real |
weighted_value_currency | text |
won_time | timestamp without time zone |
count | integer | просто поле, равное единичке везде
yandex_id | text |
google_id | text |
facebook_id | text |
offline_qualification_sent | timestamp without time zone | информация про оффлайн-квалификацию
current_tariff | text |
key_creation_date | date |
emails | ARRAY | массив емейлов; без доп манипуляций массивы не поддержаны в даталенс
phones | ARRAY | массив телефонов; без доп манипуляций массивы не поддержаны в даталенс
creator_user_id | integer |
creator_user_name | text |
user_id | integer |
user_name | text | английские имя-фамилия оунера сделки
person_id | integer |
person_name | text |
possible_duplicate_of | integer | id сделки из поля 'возможный дубль'
company_id | integer |
company_id_raw | text | строка; если несколько company_id, то они будут перечислены через запятую
organization_id | integer |
organization_name | text |
one_of_the_keys_is_active | boolean |
erp_version | text |
erp | text |
invoice | text |
login | text |
products | text |
segment | text |
year_live | integer |
orders_per_day | integer |
next_charge_date | date |


### ww_pipedrive_deals
Сделки из пайпдрайва routeq.pipedrive.com. Таблица содержит поля, которые заводятся внутри пайпдрайва, и не содержит те поля, которые мы туда заносим 'снаружи'

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
active | boolean |
activities_count | integer |
add_time | timestamp without time zone |
close_time | timestamp without time zone |
currency | text |
deleted | boolean | практически ни у кого не стоит, кажется
done_activities_count | integer |
email_messages_count | integer |
expected_close_date | date |
last_activity_date | date |
lost_reason | text |
lost_time | timestamp without time zone |
next_activity_date | date |
next_activity_id | integer |
pipeline_id | integer |
probability | real |
rotten_time | timestamp without time zone |
source | text |
stage_change_time | timestamp without time zone |
stage_id | integer |
stage_order_nr | integer |
status | text |
title | text |
undone_activities_count | integer |
update_time | timestamp without time zone |
utm_campaign | text |
utm_medium | text |
utm_source | text |
utm_term | text |
value | real |
vehicles_count | integer |
weighted_value | real |
weighted_value_currency | text |
won_time | timestamp without time zone |
count | integer | просто поле, равное единичке везде
current_tariff | text |
key_creation_date | date |
emails | ARRAY | массив емейлов; без доп манипуляций массивы не поддержаны в даталенс
phones | ARRAY | массив телефонов; без доп манипуляций массивы не поддержаны в даталенс
creator_user_id | integer |
creator_user_name | text |
user_id | integer |
user_name | text | английские имя-фамилия оунера сделки
person_id | integer |
person_name | text |
company_id | integer |
company_id_raw | text | строка; если несколько company_id, то они будут перечислены через запятую
organization_id | integer |
organization_name | text |
one_of_the_keys_is_active | boolean |
erp | text |
invoice | text |
login | text |
products | text |
segment | text |
year_live | integer |
orders_per_day | integer |
country | text |


### pipedrive_activities, ww_pipedrive_activities

Колонка | Тип | Пояснение
--- | --- | ---
activity_id | integer |
deal_id | integer |
deal_title | text |
type | text |
subject | text |
done | boolean |
user_id | integer |
owner_name | text |
add_time | timestamp without time zone |
due_date | date |
due_time | time without time zone |
update_time | timestamp without time zone |
update_user_id | integer |
marked_as_done_time | timestamp without time zone |
person_id | integer |
person_name | text |
count | integer | просто поле, равное единичке везде




### pipedrive_organizations
Организации из Пайпдрайва

Колонка | Тип | Пояснение
--- | --- | ---
org_id | integer |
name | text |
add_time | timestamp without time zone |
age | real |
website | text |
okved | text |
altay_industry | text |
altay_chain_id | bigint |
altay_chain_host | text |
altay_chain_size | integer |
company_size | text |
staff_count_info | text |
revenue | bigint |
revenue_currency | text |
owner_id | integer |
owner_name | text |
industries | ARRAY |
region | text |
area | text |
address | text |
address_formatted_address | text |
inn | bigint |


### ww_pipedrive_organizations
Организации из Пайпдрайва

Колонка | Тип | Пояснение
--- | --- | ---
org_id | integer |
name | text |
add_time | timestamp without time zone |
industries | ARRAY |
region | text |
area | text |
address | text |
address_formatted_address | text |
staff_count_info | text |
revenue | bigint |
vehicle_count | int |


### pipedrive_persons, ww_pipedrive_persons

Колонка | Тип | Пояснение
--- | --- | ---
person_id | integer |
name | text |
first_name | text |
last_name | text |
owner_id | integer |
owner_name | text |
emails | ARRAY |
phones | ARRAY |
title | text |
update_time | timestamp without time zone |
active_flag | boolean |
company_id | integer |
organization_id | integer |
organization_name | text |
roles | ARRAY |


### pipedrive_pipelines, ww_pipedrive_pipelines

Колонка | Тип | Пояснение
--- | --- | ---
pipeline_id | integer |
name | text |
url_title | text |
active | boolean |
add_time | timestamp without time zone |
update_time | timestamp without time zone |
deal_probability | boolean |
selected | boolean |


### pipedrive_stages, ww_pipedrive_stages

Колонка | Тип | Пояснение
--- | --- | ---
stage_id | integer |
stage_name | text |
pipeline_id | integer |
pipeline_name | text |
stage_order_nr | integer |
stage_active_flag | boolean |
deal_probability | real |
stage_update_time | timestamp without time zone |


### pipedrive_users, ww_pipedrive_users

Колонка | Тип | Пояснение
--- | --- | ---
user_id | integer |
name | text |
activated | boolean |
active_flag | boolean |
email | text |
is_admin | boolean |
lang | text |
locale | text |
timezone_name | text |
timezone_offset | integer |
created | timestamp without time zone |
modified | timestamp without time zone |


## apikey
### apikey_deal_id_dict
связь апи-ключей и deal_id в пайпдрайве

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
deal_id | integer |


### apikey_tariff_info
Таблица тарифов и статусов по ключам из apikeys

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
key_creation_date | date |
next_consume_date | date |
current_tariff | text |
active | boolean |


### apikey_to_client_id
Таблица соответствия между apikey и client_id

Колонка | Тип | Пояснение
--- | --- | ---
client_id | text |
apikey | text |


## backend_create_company_logs

Колонка | Тип | Пояснение
--- | --- | ---
dt | date |
iso_eventtime | timestamp without time zone |
status_code | integer |
ip | text |
endpoint | text |
method | text |
response_time_s | double precision |
url | text |
user_agent | text |
req_id | text |
service_id | text |
source | text |
source_uri | text |


## client_id_sets
Результат кластеризации запией из различных источников (pipedrive_deals, monitoring_companies) по клиентам
Записи относятся к одному клиенту, если совпадают хотя бы по одному из рассматриваемых ключей (apikey, company_id, organization_id)

Колонка | Тип | Пояснение
--- | --- | ---
client_id | text | идентификатор кластера
company_id | ARRAY | множество значений apikey, соответствующих кластеру
organization_id | ARRAY | множество значений company_id, соответствующих кластеру
apikey | ARRAY | множество значений organization_id, соответствующих кластеру


## company_id_to_client_id
Таблица соответствия между company_id и client_id

Колонка | Тип | Пояснение
--- | --- | ---
client_id | text |
company_id | integer |


## d_apikey_name

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
company_name | text |


## deal_id_to_client_id
Таблица соответствия между deal_id и client_id.
В ней могут встречаеться отрицательные значения deal_id, т.к. из всех источников кластеризации, перечисленых в CLUSTERIZATION_SOURCES в data_getters (на момент написании этого описания там есть только pipedrive_deals и monitoring_companies), поле deal_id есть только в pipedrive_deals, а для корректной работы текущей реализации кластеризации оно должно быть заполнено чем-то во всех источниках, поэтому пустые значения заполняются отрицательными.

Колонка | Тип | Пояснение
--- | --- | ---
client_id | text |
deal_id | integer |


## deal_participants

Колонка | Тип | Пояснение
--- | --- | ---
person_id | integer |
deal_id | integer |
is_primary_person | boolean |


## excel_examples_features
Таблица нужна для того, чтобы понимать, какие mvrp-запросы делались с дефолтной экселькой, а какие со своей

Колонка | Тип | Пояснение
--- | --- | ---
file_hash | text |
dt | date |
file_url | text |
depot_lat | double precision |
depot_lon | double precision |
locations_count | integer |
vehicles_count | integer |


## f_task_info
Подробная информация о mvrp-задачах

Колонка | Тип | Пояснение
--- | --- | ---
task_id | text |
apikey | text |
dt | date |
options_date | date |
status | text |
funnel_state | text |
solver_status | text |
message | text |
task_type | text |
quality | text |
solver_time_limit_s | numeric |
tasks | integer |
threads | integer |
locations | integer |
vehicles | integer |
used_vehicles | integer |
dropped_locations_count | integer |
run_on_yt | boolean |
yt_operations | json |
matrix_statistics | json |
depots | json |
count | integer |
depots_count | integer |
first_depot_lat | real |
first_depot_lon | real |
queued_ts | timestamp without time zone |
started_ts | timestamp without time zone |
matrix_downloaded_ts | timestamp without time zone |
yt_running_ts | timestamp without time zone |
yt_ready_ts | timestamp without time zone |
calculated_ts | timestamp without time zone |
completed_ts | timestamp without time zone |
error_ts | timestamp without time zone |
internal_error_ts | timestamp without time zone |
lost_ts | timestamp without time zone |
is_past | boolean |
is_manual_edit | boolean |
is_excel_example | boolean |
bucket | text |
country | text | страна первого склада
area | text | регион первого склада
city | text | город первого скалада


## marketing_spendings
Данные и метрики кампаний Яндекс.Директ и Google Ads (поля из Яндекс.Директа описаны в https://yandex.ru/dev/direct/doc/reports/fields-list.html)
Данные из Google.Ads имеют campaign_id, region_id и region_name, равный Null

Колонка | Тип | Пояснение
--- | --- | ---
dt | date | Дата, за которую приведена статистика, в формате YYYY-MM-DD
campaign_id | bigint | Идентификатор кампании, Null для Google.Ads
campaign_name | text | Название кампании
region_id | integer | Идентификатор местности кампании, Null для Google.Ads
region_name | text | Название местности кампании
impressions | integer | Количество показов
clicks | integer | Стоимость кликов
ctr | double precision | CTR, в процентах
cost | integer | Количество кликов
utm_source | text | 'Yandex.Direct' для Яндекс Директа,  'Google.Ads' для Google.Ads


## monitoring_companies
Компании курьерского Бекэнда. Почти полная копия ручки /companies

Колонка | Тип | Пояснение
--- | --- | ---
id | integer | company_id
name | text | название компании
sms_enabled | boolean | true/false
enabled_sms_types | ARRAY |
apikey | text | ключ api солвера
mark_delivered_enabled | boolean | true/false
mark_delivered_radius | real |
mark_delivered_service_time_coefficient | real |
sms_nearby_order_eta_s | integer |
optimal_order_sequence_enabled | boolean | true/false
partially_finished_status_enabled | boolean | true/false
eta_type | text |
status_presettled_comments | ARRAY |
import_depot_garage | boolean |
messenger_enabled | boolean | true/false
tracking_start_h | integer |
sms_time_window_start | time without time zone |
sms_time_window_end | time without time zone |
mvrp_enabled | boolean | true/false
monitoring_enabled | boolean | true/false
meta_company_name | text |


## monitoring_couriers
Курьеры из курьерского Бекэнда. Полная копия ручки /companies/all/couriers

Колонка | Тип | Пояснение
--- | --- | ---
id | integer | id Курьера
company_id | integer | id компании, которой принадлежит курьер
name | text | Название Курьера
number | text |
phone | text |
rating | real |
sms_enabled | boolean |


## monitoring_depots
Депо из курьерского Бекэнда. Полная копия ручки /companies/all/depots

Колонка | Тип | Пояснение
--- | --- | ---
id | integer | id Депо (не тот же id, как в mvrp задаче)
company_id | integer | id компании, которой принадлежит депо
name | text | название Депо
number | text |
address | text |
lat | real |
lon | real |
time_interval | text |
service_duration_s | real |
order_service_duration_s | real |
description | text |
time_zone | text |
allow_route_editing | boolean |
mark_route_started_radius | real |


## monitoring_depots_countries

Колонка | Тип | Пояснение
--- | --- | ---
depot_id | integer |
company_id | integer |
lat | double precision |
lon | double precision |
country | text |


## apikey_bitrix_deal_id_dict
Данные берутся из bitrix_deals, из полей uf_key, uf_key_2, uf_key_3, uf_key_4

Колонка | Тип              | Пояснение
--- |------------------| ---
deal_id | integer          | id сделки из bitrix
apikey | text               |  ключ для солвера

## monitoring_route_info
Информация об остановках в маршрутах.
//Если нужно получить все заказы, то можно пользоваться таблицей w_monitorong_orders. Она содержит те же поля, но остановки только типа order (без депо и гаражей).//

Колонка | Тип | Пояснение
--- | --- | ---
route_id | integer |
route_sequence_pos | integer |
type | text |
dt | date |
entity_id | integer |
address | text |
amount | real |
comments | text |
company_id | integer |
confirmed_at | timestamp without time zone |
customer_name | text |
delivered_at | timestamp without time zone |
depot_id | integer |
description | text |
eta_type | text |
lat | real |
lon | real |
mark_delivered_radius | real |
number | text |
payment_type | text |
phone | text |
refined_lat | real |
refined_lon | real |
service_duration_s | integer |
shared_service_duration_s | integer |
shared_with_company_ids | ARRAY |
status | text |
time_window_end | timestamp without time zone |
time_window_start | timestamp without time zone |
volume | real |
weight | real |
history_log | json |
status_log | json |
created_time | timestamp without time zone |
arrival_time | timestamp without time zone |
visit_time | timestamp without time zone |
departure_time | timestamp without time zone |


## monitoring_routes
Загруженные маршруты в мониторинг.

Колонка | Тип | Пояснение
--- | --- | ---
id | integer |
dt | date |
company_id | integer |
courier_id | integer |
depot_id | integer |
number | text |
imei | bigint |
courier_violated_route | boolean |
routing_mode | text |
tracking_start_h | integer |
route_start_s | integer |
route_finish_s | integer |


## monitoring_stat
Статистика использования мониторинга

Колонка | Тип | Пояснение
--- | --- | ---
company_id | integer |
dt | date |
n_active_couriers | integer |
n_uploaded_vehicles | integer |
n_depots | integer |
n_orders | integer |
n_orders_new | integer |
n_orders_confirmed | integer |
n_orders_postponed | integer |
n_orders_cancelled | integer |
n_orders_finished | integer |
percent_orders_finished | double precision |
company_name | text |
n_sms_new | integer |
n_sms_failed | integer |
n_sms_sent | integer |
company_id_raw | integer |
n_orders_for_couriers_with_sms | integer |
n_orders_in_nearby_sms | integer |
percent_orders_covered_by_nearby_sms | double precision |
apikey | text |


## monitoring_users
Пользователи из курьерского Бекэнда. Почти Полная копия ручки /companies/all/users

Колонка | Тип | Пояснение
--- | --- | ---
id | integer | id Пользователя
login | text | Логин пользователя (email)
confirmed_at | timestamp without time zone | время подтверждения email
is_super | boolean | true/false
role | text | Роль пользователя в компании


## monitoring_users_to_companies
Соответствие пользователей и компаний. Каждый пользователь может иметь доступ к разным компаниям.

Колонка | Тип | Пояснение
--- | --- | ---
user_id | integer |
company_id | integer |



## mvrp_stat
Статистика mvrp-запросов по api-ключу. Берется из отчета таблицы mvrp_raw_data. В качестве показателя числа успешных mvrp-запросов можно брать mvrp_reqs_200.

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
dt | date |
ts | timestamp without time zone |
mvrp_reqs | integer |
client | text | название компании; по идее, должно совпадать с пайпдрайвом; это дублирующееся поле, оно не рекомендуется к использованию, со временем выпилим его
mvrp_reqs_200 | integer |
mvrp_reqs_400 | integer |
n_distinct_locations | integer |
n_distinct_tasks | integer |
n_distinct_vehicles | integer |
reqs_200 | integer |
reqs_400 | integer |
reqs_all | integer |
svrp_reqs | integer |
svrp_reqs_200 | integer |
svrp_reqs_400 | integer |
sync_svrp_reqs | integer |
sync_svrp_reqs_200 | integer |
sync_svrp_reqs_400 | integer |
tasks_manual_future | integer |
tasks_manual_past | integer |
locations_count | integer |
reqs_without_excel_examples | integer |
tasks_auto_past | integer |
tasks_auto_future | integer |


## new_vrp_deals
На момент октября 2021 полностью совпадает с таблицей new_vrp_deals

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
active | boolean |
activities_count | integer |
add_time | timestamp without time zone |
close_time | timestamp without time zone |
currency | text |
deleted | boolean |
done_activities_count | integer |
email_messages_count | integer |
expected_close_date | date |
erp | text |
erp_version | text |
invoice | text |
last_activity_date | date |
lost_reason | text |
lost_time | timestamp without time zone |
login | text |
next_activity_date | date |
next_activity_id | integer |
orders_per_day | integer |
pipeline_id | integer |
products | text |
probability | real |
rotten_time | timestamp without time zone |
segment | text |
source | text |
stage_change_time | timestamp without time zone |
stage_id | integer |
stage_order_nr | integer |
status | text |
title | text |
undone_activities_count | integer |
update_time | timestamp without time zone |
utm_campaign | text |
utm_medium | text |
utm_source | text |
utm_term | text |
value | real |
vehicles_count | integer |
weighted_value | real |
weighted_value_currency | text |
won_time | timestamp without time zone |
count | integer |
yandex_id | text |
google_id | text |
facebook_id | text |
offline_qualification_sent | timestamp without time zone |
one_of_the_keys_is_active | boolean |
current_tariff | text |
key_creation_date | date |
year_live | integer |
emails | ARRAY |
phones | ARRAY |
creator_user_id | integer |
creator_user_name | text |
user_id | integer |
user_name | text |
person_id | integer |
person_name | text |
possible_duplicate_of | integer |
company_id | integer |
company_id_raw | text |
organization_id | integer |
organization_name | text |
add_date | date |
next_charge_date | date |


## organization_id_to_client_id
Таблица соответствия между organization_id и client_id

Колонка | Тип | Пояснение
--- | --- | ---
client_id | text |
organization_id | integer |


## sales_employees
Информация о продавцах

Колонка | Тип | Пояснение
--- | --- | ---
login | text | со стаффа
name_ru | text | со стаффа
name_en | text | имя, аналогичное имени продавца в пайпдрайве (НЕ имя со стаффа)
phone_number | text | внутренний номер со стаффа
team | text | SMB или VRP Ent Hunters
active | boolean | false если сотрудник уже не работает
sub_team | text | smb_1/smb_2/ent_1/ent_farm_1


## sales_employees_goals
Информация о планах продаж для продавцов

Колонка | Тип | Пояснение
--- | --- | ---
login | text | со стаффа
period_beg | date | начало целевого периода
period_end | date | конец целевого периода
target | integer | план продаж (в рублях) на этот период


## support_tickets
Тикеты поддержки в Самсаре

 Колонка         | Тип                         | Пояснение
-----------------|-----------------------------| ---
 channel         | text                        | канал поступления запроса, на март 2021 только EMAIL
 company_id      | integer                     |
 created         | timestamp without time zone | дата и время и создания
 dt              | date                        | дата создания, столбец нужен для правильного обновления таблицы
 email           | text                        | емейл обратившегося
 priority        | text                        | приоритет обращения ('LOW | NORMAL | CRITICAL | MAJOR')
 subject         | text                        | тема обращения
 ticket_number   | bigint                      | номер тикета
 article_created | timestamp without time zone |
 article_id      | bigint                      |


## taxi_claim_data
Таблица с информаицией о заказах такси через нас

Колонка | Тип | Пояснение
--- | --- | ---
watch_id | text | идентификатор события из таблицы hits_all
dt | date |
event_time | date |
orders_count | integer | количество вызовов
price | double precision |
params | text | это поле содержит всю инормацию, которая уходит с фронта в hits_all. на всякий случай
client_ip | text |
referer | text |
company_id | double precision |


## tel_stat
Данные из яндекс.телефонии по звонкам наших продавцов

Колонка | Тип | Пояснение
--- | --- | ---
dt | date |
ts | timestamp without time zone |
ts_connect | timestamp without time zone |
ts_disconnect | timestamp without time zone |
duration | integer |
call_direction | text |
from_number | text |
via_number | text |
to_number | text |


## vrp_apikeys_dict
можно попробовать брать данные из этой таблицы, а не из словаря
Просто занесли в DWH словарь https://stat.yandex-team.ru/DictionaryEditor/vrp_apikeys_dict , связывающий названия компаний в пайпдрайве с их апи-ключами, и добавили словарь https://stat.yandex-team.ru/DictionaryEditor/vrp_apikeys_meta_companies_dict с мета-компаниями

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
company_name | text | название из пайпдрайва
meta_company_name | text |


## vrp_depots_countries

Колонка | Тип | Пояснение
--- | --- | ---
dt | date |
rounded_lat | integer |
rounded_lon | integer |
country | text |


## ya_courier_meta_company_ids

Колонка | Тип | Пояснение
--- | --- | ---
company_id | integer |
meta_company_name | text |
meta_company_id | integer |
meta_organization_id | integer |


## weekly_ycb_courier_positions

Колонка | Тип | Пояснение
--- | --- | ---
dt | date |
id | bigint |
route_id | integer |
courier_id | integer |
time | double precision |
lat | double precision |
lon | double precision |
accuracy | double precision |
server_time | double precision |
imei | text |


## worldwide_router_shoots
Таблица с измерениями качеста OSM роутера. Каждый день стрельяется какое-то количество треков.
В таблицы лежать результаты этих обстрелов.

Колонка | Тип | Пояснение
--- | --- | ---
dt | date not null |  Дата, выстрела
key | text | ID трека пользователя `<uuid>_<номер сессии>_<номер трека>`
shooter_name | text | Роутер, на котором измерялось качество
client | text | Поставщик данных
continent | text | Континент, в котором лежит большая часть трека
country | text | Страна, в которой лежит большая часть трека
area | text | Регион, в котором лежит большая часть трека
city | text | Город, в котором лежит большая часть трека
src_lat | float | Широта точки старта
src_lon | float | Долгота точки финиша
dst_lat | float | Широта точки финиша
dst_lon | float | Долгота точки финиша
haversine | float | Расстояние между стартом и финишем `по воздуху`
rta | float | Реальное время поездки
track_len | float | Реальная длинна поездки
eta | integer | Предсказанное время поездки
predicted_len | float | Предсказанная длинна поездки
ts | integer | Время поездки (которое передавалось в роутер при выстреле)
time_of_shoot | integer | Точное время выстрела в роутер


# Views - производные таблицы, полученные из исходных таблиц

## d_calendar
Календарь дат от 2010 до 2030 года

Колонка | Тип | Пояснение
--- | --- | ---
date | date |
year | integer |
quarter | integer |
month | integer |
week | integer |
year_quarter | text |
day_of_week | integer |
first_day_of_week | date |
first_day_of_month | date |
first_day_of_quarter | date |
day_of_week_name | text |


## w_active_apikey_days

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
dt | date |


## w_active_organization_days

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
dt | date |


## w_apikey_organization_id

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
apikey | text |


## w_daily_vehicle_counts

Колонка | Тип | Пояснение
--- | --- | ---
dt | date |
apikey | text |
monitoring_vehicles | integer |
vrp_vehicles | integer |


## w_depots_used_last_month_by_apikey
Таблица, в которой можно по апиключу посмотреть, какие координаты складов использовались за последний месяц

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
depot | text | координаты депо
usages | bigint | сколько раз использовались


## w_last_activity_of_paid_organizations

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
last_activity_date | date |


## w_latest_four_calendar_weeks_active_days_percentages

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
active_days_percent | double precision |
organization_name | text |
latest_won_user_name | text |
latest_won_deal_value | real |
latest_open_user_name | text |
pipeline_id | integer |
first_won_date | date |
last_won_date | date |
won_deals_count | bigint |
organization_url | text |
active_category | text |


## w_manual_adjustments_per_week

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
year | integer |
week | integer |
n_distinct_locations_sum | bigint |
tasks_manual_future_sum | bigint |


## w_marketing_spendings_x_pipedrive_deals

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
active | boolean |
activities_count | integer |
add_time | timestamp without time zone |
close_time | timestamp without time zone |
currency | text |
deleted | boolean |
done_activities_count | integer |
email_messages_count | integer |
expected_close_date | date |
last_activity_date | date |
lost_reason | text |
lost_time | timestamp without time zone |
next_activity_date | date |
next_activity_id | integer |
pipeline_id | integer |
probability | real |
rotten_time | timestamp without time zone |
source | text |
stage_change_time | timestamp without time zone |
stage_id | integer |
stage_order_nr | integer |
status | text |
title | text |
undone_activities_count | integer |
update_time | timestamp without time zone |
utm_campaign | text |
utm_medium | text |
utm_source | text |
utm_term | text |
value | real |
vehicles_count | integer |
weighted_value | real |
weighted_value_currency | text |
won_time | timestamp without time zone |
count | integer |
yandex_id | text |
google_id | text |
facebook_id | text |
offline_qualification_sent | timestamp without time zone |
current_tariff | text |
key_creation_date | date |
emails | ARRAY |
phones | ARRAY |
creator_user_id | integer |
creator_user_name | text |
user_id | integer |
user_name | text |
person_id | integer |
person_name | text |
possible_duplicate_of | integer |
company_id | integer |
company_id_raw | text |
organization_id | integer |
organization_name | text |
one_of_the_keys_is_active | boolean |
erp_version | text |
erp | text |
invoice | text |
login | text |
products | text |
segment | text |
year_live | integer |
orders_per_day | integer |
next_charge_date | date |
campaign_id | bigint |
campaign_name | text |
dt | date |
impressions | bigint |
clicks | bigint |
cost | bigint |
marketing_spendings_utm_source | text |


## w_monitoring_orders
Все из monitoring_route_info, где type = 'order'

Колонка | Тип | Пояснение
--- | --- | ---
route_id | integer |
route_sequence_pos | integer |
type | text |
dt | date |
entity_id | integer |
address | text |
amount | real |
comments | text |
company_id | integer |
confirmed_at | timestamp without time zone |
customer_name | text |
delivered_at | timestamp without time zone |
depot_id | integer |
description | text |
eta_type | text |
lat | real |
lon | real |
mark_delivered_radius | real |
number | text |
payment_type | text |
phone | text |
refined_lat | real |
refined_lon | real |
service_duration_s | integer |
shared_service_duration_s | integer |
shared_with_company_ids | ARRAY |
status | text |
time_window_end | timestamp without time zone |
time_window_start | timestamp without time zone |
volume | real |
weight | real |
history_log | json |
status_log | json |
created_time | timestamp without time zone |
arrival_time | timestamp without time zone |
visit_time | timestamp without time zone |
departure_time | timestamp without time zone |


## w_monitoring_quality_weekly

Колонка | Тип | Пояснение
--- | --- | ---
name | text |
company_id | integer |
week_start | date |
perc_completed_orders | numeric |
perc_active_routes | numeric |
perc_violated_routes | numeric |


## w_mvrp_and_monitoring_stat

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
dt | date |
ts | timestamp without time zone |
mvrp_reqs | integer |
client | text |
mvrp_reqs_200 | integer |
mvrp_reqs_400 | integer |
n_distinct_locations | integer |
n_distinct_tasks | integer |
n_distinct_vehicles | integer |
reqs_200 | integer |
reqs_400 | integer |
reqs_all | integer |
svrp_reqs | integer |
svrp_reqs_200 | integer |
svrp_reqs_400 | integer |
sync_svrp_reqs | integer |
sync_svrp_reqs_200 | integer |
sync_svrp_reqs_400 | integer |
company_id | integer |
n_active_couriers | integer |
n_uploaded_vehicles | integer |
n_depots | integer |
n_orders | integer |
n_orders_new | integer |
n_orders_confirmed | integer |
n_orders_postponed | integer |
n_orders_cancelled | integer |
n_orders_finished | integer |
percent_orders_finished | double precision |
company_name | text |
n_sms_new | integer |
n_sms_failed | integer |
n_sms_sent | integer |
company_id_raw | integer |
n_orders_for_couriers_with_sms | integer |
n_orders_in_nearby_sms | integer |
percent_orders_covered_by_nearby_sms | double precision |


## w_mvrp_stat_extended
mvrp-статистика с учетом ручных редактирований из прошлого/будущего
(На момент октября 2021 полностью совпадает с таблицей mvrp_stat)

Колонка | Тип | Пояснение
--- | --- | ---
apikey | text |
dt | date |
ts | timestamp without time zone |
mvrp_reqs | integer |
client | text |
mvrp_reqs_200 | integer |
mvrp_reqs_400 | integer |
n_distinct_locations | integer |
n_distinct_tasks | integer |
n_distinct_vehicles | integer |
reqs_200 | integer |
reqs_400 | integer |
reqs_all | integer |
svrp_reqs | integer |
svrp_reqs_200 | integer |
svrp_reqs_400 | integer |
sync_svrp_reqs | integer |
sync_svrp_reqs_200 | integer |
sync_svrp_reqs_400 | integer |
tasks_manual_future | integer |
tasks_manual_past | integer |
locations_count | integer |
reqs_without_excel_examples | integer |
tasks_auto_past | integer |
tasks_auto_future | integer |


## w_new_vrp_deals
'Новые'сделки в пайпдрайве с моментом их добавления.
Берем сделки из пайпдрайва из воронок enterprise, smb, cold calls, self service for smb; убираем renewal, перерасходы, лост-ризон duplicate; убираем сделки, для которых есть более ранняя сделка с таким же apikey.
(На момент октября 2021 полностью совпадает с таблицей new_vrp_deals)

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
active | boolean |
activities_count | integer |
add_time | timestamp without time zone |
close_time | timestamp without time zone |
currency | text |
deleted | boolean |
done_activities_count | integer |
email_messages_count | integer |
expected_close_date | date |
erp | text |
erp_version | text |
invoice | text |
last_activity_date | date |
lost_reason | text |
lost_time | timestamp without time zone |
login | text |
next_activity_date | date |
next_activity_id | integer |
orders_per_day | integer |
pipeline_id | integer |
products | text |
probability | real |
rotten_time | timestamp without time zone |
segment | text |
source | text |
stage_change_time | timestamp without time zone |
stage_id | integer |
stage_order_nr | integer |
status | text |
title | text |
undone_activities_count | integer |
update_time | timestamp without time zone |
utm_campaign | text |
utm_medium | text |
utm_source | text |
utm_term | text |
value | real |
vehicles_count | integer |
weighted_value | real |
weighted_value_currency | text |
won_time | timestamp without time zone |
count | integer |
yandex_id | text |
google_id | text |
facebook_id | text |
offline_qualification_sent | timestamp without time zone |
one_of_the_keys_is_active | boolean |
current_tariff | text |
key_creation_date | date |
year_live | integer |
emails | ARRAY |
phones | ARRAY |
creator_user_id | integer |
creator_user_name | text |
user_id | integer |
user_name | text |
person_id | integer |
person_name | text |
possible_duplicate_of | integer |
company_id | integer |
company_id_raw | text |
organization_id | integer |
organization_name | text |
add_date | date |
next_charge_date | date |


## w_org_id_to_quasi_pipeline_id

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
pipeline_id | integer |


## w_organization_vehicle_counts

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
dt | date |
monitoring_vehicles | numeric |
vrp_vehicles | numeric |


## w_paid_routing_deals
Все выигранные сделки с ненулевой суммой в пайплайнах Small leads, Enterprise pipeline и Self-Service. Таблица представляет собой отфильтрованные pipedrive_deals с добавлением двух столбцов - won_latest и added_latest

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
active | boolean |
activities_count | integer |
add_time | timestamp without time zone |
close_time | timestamp without time zone |
currency | text |
deleted | boolean |
done_activities_count | integer |
email_messages_count | integer |
expected_close_date | date |
last_activity_date | date |
lost_reason | text |
lost_time | timestamp without time zone |
next_activity_date | date |
next_activity_id | integer |
pipeline_id | integer |
probability | real |
rotten_time | timestamp without time zone |
source | text |
stage_change_time | timestamp without time zone |
stage_id | integer |
stage_order_nr | integer |
status | text |
title | text |
undone_activities_count | integer |
update_time | timestamp without time zone |
utm_campaign | text |
utm_medium | text |
utm_source | text |
utm_term | text |
value | real |
vehicles_count | integer |
weighted_value | real |
weighted_value_currency | text |
won_time | timestamp without time zone |
count | integer |
yandex_id | text |
google_id | text |
facebook_id | text |
offline_qualification_sent | timestamp without time zone |
current_tariff | text |
key_creation_date | date |
emails | ARRAY |
phones | ARRAY |
creator_user_id | integer |
creator_user_name | text |
user_id | integer |
user_name | text |
person_id | integer |
person_name | text |
possible_duplicate_of | integer |
company_id | integer |
company_id_raw | text |
organization_id | integer |
organization_name | text |
one_of_the_keys_is_active | boolean |
erp_version | text |
erp | text |
invoice | text |
login | text |
products | text |
segment | text |
year_live | integer |
orders_per_day | integer |
next_charge_date | date |
won_first | boolean |
added_first | boolean |
won_latest | boolean | true/false, флаг что данная сделка является последней выигранной для данной организации
added_latest | boolean | true/false, флаг что данная сделка является последней созданной для данной организации


## w_paid_routing_deals_contacts
все люди всех выигранных сделок с ненулевой суммой в пайплайнах Small leads, Enterprise pipeline и Self-Service с контактами.

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer |
deal_title | text |
value | real |
organization_id | integer |
organization_name | text |
add_time | timestamp without time zone |
added_latest | boolean | true/false, флаг что данная сделка является последней созданной для данной организации
won_time | timestamp without time zone |
won_latest | boolean | true/false, флаг что данная сделка является последней созданной для данной организации
pipeline_id | integer |
pipeline_name | text |
person_id | integer |
name | text |
is_primary_person | boolean | является ли данный Person основным Person данной сделки (true), либо это один из отстальных Participants (false)
emails | ARRAY | список всех емейлов человека
phones | ARRAY | список всех телефонов человека
first_email | text | первый емейл в списке. Если есть primary емейл, то это он
first_phone | text | первый телефон в списке. Если есть primary телефон, то это он


## w_paid_routing_organizations

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
organization_name | text |
latest_won_user_name | text |
latest_won_deal_value | real |
latest_open_user_name | text |
pipeline_id | integer |
first_won_date | date |
last_won_date | date |
won_deals_count | bigint |
organization_url | text |


## w_paid_routing_organizations_test

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
organization_name | text |
latest_won_user_name | text |
latest_won_deal_value | real |
pipeline_id | integer |
first_won_date | date |
last_won_date | date |
won_deals_count | bigint |
organization_url | text |


## w_paid_routing_organizations_v2

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
organization_name | text |
latest_won_user_name | text |
latest_won_deal_value | real |
latest_open_user_name | text |
pipeline_id | integer |
first_won_date | date |
last_won_date | date |
won_deals_count | bigint |
organization_url | text |


## w_quasi_routing_pipelines

Колонка | Тип | Пояснение
--- | --- | ---
pipeline_id | integer |
name | text |
url_title | text |
active | boolean |
add_time | timestamp without time zone |
update_time | timestamp without time zone |
deal_probability | boolean |
selected | boolean |


## w_relevant_org_id_week_pairs

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
first_day_of_week | date |


## w_routing_churn

Колонка | Тип | Пояснение
--- | --- | ---
pipeline_id | integer |
organizations_count | bigint |
churn_percent | double precision |


## w_task_info_extended
Таблица f_task_info с информацией о ручных редактированиях (перерешиваниях, корректировках)

Колонка | Тип | Пояснение
--- | --- | ---
task_id | text |
apikey | text |
dt | date |
options_date | date |
status | text |
funnel_state | text |
solver_status | text |
message | text |
task_type | text |
quality | text |
solver_time_limit_s | numeric |
tasks | integer |
threads | integer |
locations | integer |
vehicles | integer |
used_vehicles | integer |
dropped_locations_count | integer |
run_on_yt | boolean |
yt_operations | json |
matrix_statistics | json |
depots | json |
count | integer |
depots_count | integer |
first_depot_lat | real |
first_depot_lon | real |
queued_ts | timestamp without time zone |
started_ts | timestamp without time zone |
matrix_downloaded_ts | timestamp without time zone |
yt_running_ts | timestamp without time zone |
yt_ready_ts | timestamp without time zone |
calculated_ts | timestamp without time zone |
completed_ts | timestamp without time zone |
error_ts | timestamp without time zone |
internal_error_ts | timestamp without time zone |
lost_ts | timestamp without time zone |
is_past | boolean |
is_manual_edit | boolean |
is_excel_example | boolean |
bucket | text |


## w_vehicles_report

Колонка | Тип | Пояснение
--- | --- | ---
meta_client | text |
company_id | integer |
apikey | text |
dt | date |
ts | timestamp without time zone |
mvrp_reqs | integer |
client | text |
mvrp_reqs_200 | integer |
mvrp_reqs_400 | integer |
n_distinct_locations | integer |
n_distinct_tasks | integer |
n_distinct_vehicles | integer |
reqs_200 | integer |
reqs_400 | integer |
reqs_all | integer |
svrp_reqs | integer |
svrp_reqs_200 | integer |
svrp_reqs_400 | integer |
sync_svrp_reqs | integer |
sync_svrp_reqs_200 | integer |
sync_svrp_reqs_400 | integer |
tasks_manual_future | integer |
tasks_manual_past | integer |
locations_count | integer |
reqs_without_excel_examples | integer |
tasks_auto_past | integer |
tasks_auto_future | integer |
n_active_couriers | integer |
n_uploaded_vehicles | integer |
n_depots | integer |
n_orders | integer |
n_orders_new | integer |
n_orders_confirmed | integer |
n_orders_postponed | integer |
n_orders_cancelled | integer |
n_orders_finished | integer |
percent_orders_finished | double precision |
company_name | text |
n_sms_new | integer |
n_sms_failed | integer |
n_sms_sent | integer |
company_id_raw | integer |
n_orders_for_couriers_with_sms | integer |
n_orders_in_nearby_sms | integer |
percent_orders_covered_by_nearby_sms | double precision |
company_name_from_apikeys_dict | text |
meta_company_name_mvrp | text |
company_name_monitoring | text |
meta_company_name_monitoring | text |
vehicles_on_platform | integer |
vehicles_on_platform_sum | integer |
locations_on_platform | integer |
locations_on_platform_sum | integer |
client_rank | bigint |
client_locations_rank | bigint |


## w_vehicles_report_worldwide

Колонка | Тип | Пояснение
--- | --- | ---
meta_client | text |
company_id | integer |
apikey | text |
dt | date |
ts | timestamp without time zone |
mvrp_reqs | integer |
client | text |
mvrp_reqs_200 | integer |
mvrp_reqs_400 | integer |
n_distinct_locations | integer |
n_distinct_tasks | integer |
n_distinct_vehicles | integer |
reqs_200 | integer |
reqs_400 | integer |
reqs_all | integer |
svrp_reqs | integer |
svrp_reqs_200 | integer |
svrp_reqs_400 | integer |
sync_svrp_reqs | integer |
sync_svrp_reqs_200 | integer |
sync_svrp_reqs_400 | integer |
tasks_manual_future | integer |
tasks_manual_past | integer |
locations_count | integer |
reqs_without_excel_examples | integer |
tasks_auto_past | integer |
tasks_auto_future | integer |
n_active_couriers | integer |
n_uploaded_vehicles | integer |
n_depots | integer |
n_orders | integer |
n_orders_new | integer |
n_orders_confirmed | integer |
n_orders_postponed | integer |
n_orders_cancelled | integer |
n_orders_finished | integer |
percent_orders_finished | double precision |
company_name | text |
n_sms_new | integer |
n_sms_failed | integer |
n_sms_sent | integer |
company_id_raw | integer |
n_orders_for_couriers_with_sms | integer |
n_orders_in_nearby_sms | integer |
percent_orders_covered_by_nearby_sms | double precision |
company_name_from_apikeys_dict | text |
meta_company_name_mvrp | text |
company_name_monitoring | text |
meta_company_name_monitoring | text |
vehicles_on_platform | integer |
vehicles_on_platform_sum | integer |
locations_on_platform | integer |
locations_on_platform_sum | integer |
client_rank | bigint |
client_locations_rank | bigint |


## w_vrp_and_monitoring_vehicles_stat

Колонка | Тип | Пояснение
--- | --- | ---
dt | date |
apikey | text |
monitoring_vehicles | integer |
vrp_vehicles | integer |


## w_vrp_retention
Таблица для построения отчета по ретеншену

Колонка | Тип | Пояснение
--- | --- | ---
add_date | date |
days_after_deal_added | integer |
active_deals_count | bigint |
percent_active | numeric |


## w_weekly_organizations_vehicles_counts

Колонка | Тип | Пояснение
--- | --- | ---
organization_id | integer |
first_day_of_week | date |
weekly_average_used_vehicles | numeric |


## pipedrive_time_in_stages, ww_pipedrive_time_in_stages

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | integer | ID сделки
stage_id | integer | ID стадии
stage_duration_minutes | integer | время проведенное на стадии
came_into_stage_time | timestamp | момент попадания в стадию (если сделака там не первый раз, то последний из них)
got_out_stage_time | timestamp | момент выхода из стадии (если сделака там не первый раз, то последний из них, если она все еще там, то None)


## monitoring_depots_regions

Колонка | Тип | Пояснение
--- | --- | ---
depot_id | integer | ID склада в бекенде (первичный ключ)
company_id | integer | ID компании в  бекенде
lat | float | широта склада
lon | float | долгота склада
country | text | страна склада
area | text | регион склада
city | text | город склада


## w_pipedrive_deals_extended
Расширение таблицы pipedrive_deals: к таблице pipedrive_deals приджойнены справочники pipedrive_stages и
pipedrive_pipelines, добавлены поля:

Колонка | Тип | Пояснение
--- | --- | ---
is_relevant | integer | 1, если title сделки не сожержит renewal, перерасход, limits, Export; 0 иначе
is_qualified | text |  квалифицированная ли сделка: 'qualified', если квалифицирована, 'qualification', если проходит стадию
активной квалификации, 'not qualified', если сделка не явялется квалифицированной.


## w_marketing_campaigns_stat
Статистика рекламных кампаний с группировкой по кампании, дате и источнике

Колонка | Тип | Пояснение
--- | --- | ---
campaign_name | text | название кампании
dt | date | дата статистики
impressions | integer | кол-во показов
clicks | integer | кол-во кликов
cost | float | стоимость кампании
marketing_spendings_utm_source | text | 'yandex' при Яндекс.Директе, 'google' при Google.Ads, иначе Null


##w_marketing_campaigns_stat_deals
Статистика рекламных кампаний с количеством квалифицированных сделок и разбивкой по кол-ву машин. Кроме всех полей
w_marketing_campaigns_stat содержит

Колонка | Тип | Пояснение
--- | --- | ---
deals_num | integer | кол-во сделок за этот день по этой кампании для этого источника
qualified_num | integer | кол-во квалифицированных сделок
qualification_num | integer | кол-во сделок в стадии активной квалификации
not_qualified_num | integer | кол-во не квал. сделок
vehicles_num | integer | кол-во машин в сделке, берется n из (n-m) в тайтле сделки, если тайтл не заполнен, берется нижний порог по пайплайну
vehicles_1_2 | integer | кол-во сделок c 1-2 машинами
vehicles_3_10 | integer |
vehicles_11_20 | integer |
vehicles_21_50 | integer |
vehicles_51_100 | integer |
vehicles_100_499 | integer |
vehicles_500 | integer |


## task_id_to_origin
Для каждого task_id узнаем, запустили ли эту задачу с помощью api или ui

Колонка | Тип | Пояснение
--- | --- | ---
task_id | string |
apikey | string | apikey, с которого запущена задача
dt | date | дата запуска задачи
origin_ui | bool | true, если запущено через ui



## revenue
Данные из соответствующего гуглодока о финансовых поступлениях

Колонка | Тип | Пояснение
--- | --- | ---
client | string | Наименование клиента
payer | string | Наименование плательщика
transaction_date | date | дата платежа
account_number | string | номер счета
value | float | сумма(руб)
product_name | string | название сервис
period | int | на какой срок куплено
is_paid | string | оплачен да/нет
type | string | тип сделки (new/renewal/over)
is_offer | string | оферта/не оферта
manager | string | менеджер
sales_group | string | smb/ent/ww
maps_or_routeq | string | карты/маршрутизация
sale_location | string | Россия/снг/мир
deal_id | integer |


w_mrr_revenue
Вьюха с MRR значениями revenue

Колонка | Тип | Пояснение
--- | --- | ---
client | string | Наименование клиента
payer | string | Наименование плательщика
transaction_date | date | дата платежа
account_number | string | номер счета
value | float | сумма(руб)
product_name | string | название сервис
period | int | на какой срок куплено
is_paid | string | оплачен да/нет
type | string | тип сделки (new/renewal/over)
is_offer | string | оферта/не оферта
manager | string | менеджер
sales_group | string | smb/ent/ww
maps_or_routeq | string | карты/маршрутизация
sale_location | string | Россия/снг/мир
deal_id | integer |
month_num | integer | порядковый номер оплаченного месяца
month | date | дата первого дня месяца
month_cost | float | value/period

w_mrr_revenue_pivot
Вьюха с MRR значениями по менеджерам и по типам

Колонка | Тип | Пояснение
--- |---| ---
type | string | new/renewal/over
sales_group | string | ent/smb
month | date | месяц платежа
prev_month | date | предыдущий месяц
manager | string | manager
mrr | float | сумма  mrr
mrr_prev_month | float | сумма  mrr в предыдущем месяце

w_revenue_pivot
Вьюха с MRR значениями по менеджерам и по типам

Колонка | Тип | Пояснение
--- |---| ---
sales_group | string | ent/smb
manager | string | manager
month | date | месяц платежа
prev_month | date | предыдущий месяц
type | string | new/renewal/over
value | float | сумма за месяц
value_prev_month | float | сумма за предыдущий месяц

for_avg_and_max_ALL_activities_due_date
Вьюха для построения таблицы со средними и масимальными значениями числа активностей сейлзов по неделям (в международке)

Колонка | Тип | Пояснение
--- | --- | ---
owner_name | string | Имя сейлза
week_end | date | Конец недели, для которой посчитано число активностей
type_corrected | string | Тип активности
count_of_activities | int | Число активностей за соответствующую неделю


funnel_mckinsey_2
Вьюха для построения графика воронки в международке.
Смысл вьюхи - информация о последнем изменении стадии каждой сделки, произошедшем до last_week_end (это даты концов недель (суббот)).


Колонка | Тип | Пояснение
--- | --- | ---
deal_id              | integer                    |ID сделки
stage_id             | integer                    |ID стадии
got_out_stage_time   | timestamp without time zone|Время ухода со стадии (последнее до week_end_change)
came_into_stage_time | timestamp without time zone|Время прихода на стадию (последнее до week_end_change)
came_into_stage_date | date                       |Дата прихода на стадию (последнее до week_end_change)
orders_for_mckinsey  | integer                    |Сгенерированные порядки стадии для того чтобы нарисовать кумулятивный график в даталенсе (например, чтобы сделка с порядком стадии 10 так же была учтена как будто она также находится на всех предыдущих стадиях), поле носит вспомогательный характер и информации не несет
week_end_change      | date                       |Дата конца недели, к которой относится изменение стадии сделки произошедшее до конца этой недели
stage_order_nr       | integer                    |Порядок стадии
close_time           | timestamp without time zone|Дата закрытия сделки
lost_time            | timestamp without time zone|Дата проигрыша сделки
won_time             | timestamp without time zone|Дата выигрыша сделки
country              | text                       |Страна
user_name            | text                       |Имя сейлза
stage_id_previous    | integer                    |Порядок предыдущей стадии
stage_order_previous | integer                    |Порядок текущей стадии
last_week_end        | date                       |Дата конца недели, которую мы рассматриваем (для которой рисуется график, то есть которую выбираем селектором)
status_for_this_date | text                       |Статус на дату last_week_end


for_avg_and_max_key_activities
Вьюха для построения таблицы со средними и масимальными значениями числа активностей сейлзов по неделям (в международке).
Отличается от for_avg_and_max_ALL_activities_due_date тем, что здесь активности - это движение сделки вперед по стадиям.

Колонка | Тип | Пояснение
--- | --- | ---
user_name | string | Имя сейлза
week_end | date | Конец недели, для которой посчитано число активностей
type | string | Тип активности
count_of_activities | int | Число активностей за соответствующую неделю



## magic_button_usage
информация по каждому использованию кнопки 'оптимизировать'

Колонка | Тип | Пояснение
--- | --- | ---
dt | date | дата лога
company_id | int |
usage | int | количество использований кнопки компанией за конкретную дату


## Bitrix таблички
### bitrix_deals
Сделки из битрикса.

Колонка | Тип | Пояснение
--- | --- | ---
ID  |  INTEGER PRIMARY KEY NOT NULL  |  ID
TITLE  |  TEXT  |  Название
TYPE_ID  |  TEXT  |  Тип
CATEGORY_ID  |  INTEGER  |  Направление
STAGE_ID  |  TEXT  |  Стадия сделки
STAGE_SEMANTIC_ID  |  TEXT  |  Группа стадии
IS_NEW  |  BOOLEAN  |  Новая сделка
IS_RECURRING  |  BOOLEAN  |  Регулярная сделка
IS_RETURN_CUSTOMER  |  BOOLEAN  |  Повторная сделка
IS_REPEATED_APPROACH  |  BOOLEAN  |  Повторное обращение
PROBABILITY  |  INTEGER  |  Вероятность
CURRENCY_ID  |  TEXT  |  Валюта
OPPORTUNITY  |  FLOAT8  |  Сумма
IS_MANUAL_OPPORTUNITY  |  BOOLEAN  |  IS_MANUAL_OPPORTUNITY
TAX_VALUE  |  FLOAT8  |  Ставка налога
COMPANY_ID  |  INTEGER  |  Компания
CONTACT_ID  |  INTEGER  |  Контакт
QUOTE_ID  |  TEXT  |  Предложение
BEGINDATE  |  DATE  |  Дата начала
CLOSEDATE  |  DATE  |  Дата завершения
TRUE_BEGINDATE | DATE  | Дата начала сделки (действительно и для сделок, переехавших  из pipedrive, и для сделок, созданных bitrix)
TRUE_CLOSEDATE  | DATE  | Дата закрытия сделки (действительно и для сделок, переехавших  из pipedrive, и для сделок, созданных bitrix)
OPENED  |  BOOLEAN  |  Доступна для всех
CLOSED  |  BOOLEAN  |  Закрыта
COMMENTS  |  TEXT  |  Комментарий
ASSIGNED_BY_ID  |  INTEGER  |  Ответственный
CREATED_BY_ID  |  INTEGER  |  Кем создана
MODIFY_BY_ID  |  INTEGER  |  Кем изменена
DATE_CREATE  |  TIMESTAMP  |  Дата создания
DATE_MODIFY  |  TIMESTAMP  |  Дата изменения
SOURCE_ID  |  TEXT  |  Источник
SOURCE_DESCRIPTION  |  TEXT  |  Дополнительно об источнике
LEAD_ID  |  TEXT  |  Лид
ADDITIONAL_INFO  |  TEXT  |  Дополнительная информация
LOCATION_ID  |  TEXT  |  Местоположение
ORIGINATOR_ID  |  TEXT  |  Внешний источник
ORIGIN_ID  |  TEXT  |  Идентификатор элемента во внешнем источнике
UTM_SOURCE  |  TEXT  |  Рекламная система
UTM_MEDIUM  |  TEXT  |  Тип трафика
UTM_CAMPAIGN  |  TEXT  |  Обозначение рекламной кампании
UTM_CONTENT  |  TEXT  |  Содержание кампании
UTM_TERM  |  TEXT  |  Условие поиска кампании
UF_PIPEDRIVE_ID  |  TEXT  |  ID в Pipedrive
UF_NUM_VEHICLES  |  INTEGER  |  # of vehicles
UF_NUM_ORDERS  |  INTEGER  |  # of orders
UF_LOGIN  |  TEXT  |  Login
UF_INVOICE  |  TEXT  |  Invoice / Счёт # (ЛС-/Б-/EU-)
UF_CONTRACT_NUM  |  TEXT  |  Contract #
UF_CONTRACT_TICKET  |  TEXT  |  Contracting ticket
UF_CONDITION  |  TEXT  |  Состояние
UF_DATE_CREATED  |  TIMESTAMP  |  Дата создания
UF_DATE_CLOSED  |  TIMESTAMP  |  Сделка закрыта
UF_OFFER_CONTRACT  |  TEXT  |  Оферта или договор?
UF_YEAR_LIVE  |  FLOAT8  |  Year live
UF_ERP_VERSION  |  TEXT  |  ERP version
UF_ERP  |  TEXT  |  ERP
UF_SUBSCR_TYPE  |  TEXT  |  Subscription type
UF_DEAL_TYPE  |  TEXT  |  Deal Type
UF_SOURCE  |  TEXT  |  Source
UF_COMPETITORS  |  TEXT  |  Конкуренты
UF_RENEWAL_DATE  |  DATE  |  Contract Renewal Date
UF_KEY  |  TEXT  |  Key
UF_KEY_2  |  TEXT  |  Key2
UF_KEY_3  |  TEXT  |  Key3
UF_KEY_4  |  TEXT  |  Key3
UF_NEED_FLEET  |  BOOLEAN  |  Need fleet
UF_REQ_FIRST_DATE  |  DATE  |  Дата первого запроса
UF_REQ_LAST_DATE  |  DATE  |  Дата последнего запроса
UF_MVPR_REQ  |  INTEGER  |  Число запросов MVRP за месяц
UF_MVPR_DAYS  |  INTEGER  |  Число дней с запросами MVRP за месяц
UF_COMPANY_ID  |  INTEGER  |  company_id
UF_PRODUCT_REQ  |  INTEGER  |  Product requests
UF_DUPLICATES  |  TEXT  |  Возможный дубль (deal ID)
UF_TELESALES  |  BOOLEAN  |  Telesales
UF_UTM_SOURCE  |  TEXT  |  utm_source
UF_UTM_CONTENT  |  TEXT  |  utm_content
UF_UTM_CAMPAIGN  |  TEXT  |  utm_campaign
UF_UTM_MEDIUM  |  TEXT  |  utm_medium
UF_UTM_TERM  |  TEXT  |  utm_term
UF_YANDEX_ID  |  INTEGER  |  Yandex ID
UF_GOOGLE_ID  |  INTEGER  |  Google ID
UF_FACEBOOK_ID  |  INTEGER  |  Facebook ID
UF_OFFLINE_QUAL_SENT  |  DATE  |  offline_qualification_sent
UF_KEY_DATE  |  DATE  |  Дата создания действующего ключа
UF_CUR_TARIFF  |  TEXT  |  Текущий тариф
UF_HAS_ACTIVE_KEY  |  BOOLEAN  |  Есть ли активный ключ
UF_SCORE  |  FLOAT8  |  Score
UF_NEXT_CHARGE_DATE  |  DATE  |  Next charge date
UF_TICKET  |  TEXT  |  Тикет на внедрение
UF_STATUS  |  TEXT  |  Status
UF_CLIENT_FORM  |  TEXT  |  Форма квалификации крупного клиента
UF_ACCOUNT_MANAGER  |  TEXT  |  Account Manager
UF_CRM_1649850069082  |  TEXT  |  Тикет на внедрение
PLANNING_CLOSEDATE   | DATE  | Планируемая дата закрытия сделки


### bitrix_companies
Компании из битрикса

Колонка | Тип | Пояснение
--- | --- | ---
ID  |  INTEGER PRIMARY KEY NOT NULL  |  ID
TITLE  |  TEXT  |  Название
TYPE_ID  |  TEXT  |  Тип
CATEGORY_ID  |  INTEGER  |  Направление
STAGE_ID  |  TEXT  |  Стадия сделки
STAGE_SEMANTIC_ID  |  TEXT  |  Группа стадии
IS_NEW  |  BOOLEAN  |  Новая сделка
IS_RECURRING  |  BOOLEAN  |  Регулярная сделка
IS_RETURN_CUSTOMER  |  BOOLEAN  |  Повторная сделка
IS_REPEATED_APPROACH  |  BOOLEAN  |  Повторное обращение
PROBABILITY  |  INTEGER  |  Вероятность
CURRENCY_ID  |  TEXT  |  Валюта
OPPORTUNITY  |  FLOAT8  |  Сумма
IS_MANUAL_OPPORTUNITY  |  BOOLEAN  |  IS_MANUAL_OPPORTUNITY
TAX_VALUE  |  FLOAT8  |  Ставка налога
COMPANY_ID  |  INTEGER  |  Компания
CONTACT_ID  |  INTEGER  |  Контакт
QUOTE_ID  |  TEXT  |  Предложение
BEGINDATE  |  DATE  |  Дата начала
CLOSEDATE  |  DATE  |  Дата завершения
OPENED  |  BOOLEAN  |  Доступна для всех
CLOSED  |  BOOLEAN  |  Закрыта
COMMENTS  |  TEXT  |  Комментарий
ASSIGNED_BY_ID  |  INTEGER  |  Ответственный
CREATED_BY_ID  |  INTEGER  |  Кем создана
MODIFY_BY_ID  |  INTEGER  |  Кем изменена
DATE_CREATE  |  TIMESTAMP  |  Дата создания
DATE_MODIFY  |  TIMESTAMP  |  Дата изменения
SOURCE_ID  |  TEXT  |  Источник
SOURCE_DESCRIPTION  |  TEXT  |  Дополнительно об источнике
LEAD_ID  |  TEXT  |  Лид
ADDITIONAL_INFO  |  TEXT  |  Дополнительная информация
LOCATION_ID  |  TEXT  |  Местоположение
ORIGINATOR_ID  |  TEXT  |  Внешний источник
ORIGIN_ID  |  TEXT  |  Идентификатор элемента во внешнем источнике
UTM_SOURCE  |  TEXT  |  Рекламная система
UTM_MEDIUM  |  TEXT  |  Тип трафика
UTM_CAMPAIGN  |  TEXT  |  Обозначение рекламной кампании
UTM_CONTENT  |  TEXT  |  Содержание кампании
UTM_TERM  |  TEXT  |  Условие поиска кампании
UF_PIPEDRIVE_ID  |  TEXT  |  ID в Pipedrive
UF_NUM_VEHICLES  |  INTEGER  |  # of vehicles
UF_NUM_ORDERS  |  INTEGER  |  # of orders
UF_LOGIN  |  TEXT  |  Login
UF_INVOICE  |  TEXT  |  Invoice / Счёт # (ЛС-/Б-/EU-)
UF_CONTRACT_NUM  |  TEXT  |  Contract #
UF_CONTRACT_TICKET  |  TEXT  |  Contracting ticket
UF_CONDITION  |  TEXT  |  Состояние
UF_DATE_CREATED  |  TIMESTAMP  |  Дата создания
UF_DATE_CLOSED  |  TIMESTAMP  |  Сделка закрыта
UF_OFFER_CONTRACT  |  TEXT  |  Оферта или договор?
UF_YEAR_LIVE  |  FLOAT8  |  Year live
UF_ERP_VERSION  |  TEXT  |  ERP version
UF_ERP  |  TEXT  |  ERP
UF_SUBSCR_TYPE  |  TEXT  |  Subscription type
UF_DEAL_TYPE  |  TEXT  |  Deal Type
UF_SOURCE  |  TEXT  |  Source
UF_COMPETITORS  |  TEXT  |  Конкуренты
UF_RENEWAL_DATE  |  DATE  |  Contract Renewal Date
UF_KEY  |  TEXT  |  Key
UF_KEY_2  |  TEXT  |  Key2
UF_KEY_3  |  TEXT  |  Key3
UF_KEY_4  |  TEXT  |  Key3
UF_NEED_FLEET  |  BOOLEAN  |  Need fleet
UF_REQ_FIRST_DATE  |  DATE  |  Дата первого запроса
UF_REQ_LAST_DATE  |  DATE  |  Дата последнего запроса
UF_MVPR_REQ  |  INTEGER  |  Число запросов MVRP за месяц
UF_MVPR_DAYS  |  INTEGER  |  Число дней с запросами MVRP за месяц
UF_COMPANY_ID  |  INTEGER  |  company_id
UF_PRODUCT_REQ  |  INTEGER  |  Product requests
UF_DUPLICATES  |  TEXT  |  Возможный дубль (deal ID)
UF_TELESALES  |  BOOLEAN  |  Telesales
UF_UTM_SOURCE  |  TEXT  |  utm_source
UF_UTM_CONTENT  |  TEXT  |  utm_content
UF_UTM_CAMPAIGN  |  TEXT  |  utm_campaign
UF_UTM_MEDIUM  |  TEXT  |  utm_medium
UF_UTM_TERM  |  TEXT  |  utm_term
UF_YANDEX_ID  |  INTEGER  |  Yandex ID
UF_GOOGLE_ID  |  INTEGER  |  Google ID
UF_FACEBOOK_ID  |  INTEGER  |  Facebook ID
UF_OFFLINE_QUAL_SENT  |  DATE  |  offline_qualification_sent
UF_KEY_DATE  |  DATE  |  Дата создания действующего ключа
UF_CUR_TARIFF  |  TEXT  |  Текущий тариф
UF_HAS_ACTIVE_KEY  |  BOOLEAN  |  Есть ли активный ключ
UF_SCORE  |  FLOAT8  |  Score
UF_NEXT_CHARGE_DATE  |  DATE  |  Next charge date
UF_TICKET  |  TEXT  |  Тикет на внедрение
UF_STATUS  |  TEXT  |  Status
UF_CLIENT_FORM  |  TEXT  |  Форма квалификации крупного клиента
UF_ACCOUNT_MANAGER  |  TEXT  |  Account Manager
UF_CRM_1649850069082  |  TEXT  |  Тикет на внедрение
UF_NEXT_RENEWAL_DATE | DATE |   Дата продления лицензии
UF_RESPONSIBLE_PERSON  | INTEGER | Ответственный за компанию
UF_FULL_COMPANY_NAME | TEXT  | Полное наименование компании
UF_SCORING_PR | FLOAT8  |  Скоринг компании по PR
UF_SCORING_UPSELL | FLOAT8  |  Скоринг компании по Upsell
UF_SCORING_EFFORT | FLOAT8  | Скоринг компании по Effort
UF_SCORING_RENEWAL | FLOAT8  |  Скоринг компании по Renewal
UF_SCORING_TOTAL | FLOAT8  |  Сумма оценок (скорингов) компании
UF_ARR_MONTHLY | TEXT  |  Сумма выручки по клиенту в месяц (с указанием валюты)


### bitrix_activities
Активности из битрикса

Колонка | Тип | Пояснение
--- | --- | ---
ID  |  INTEGER PRIMARY KEY NOT NULL  |  ID
OWNER_ID  |  INTEGER  |  ID владельца
OWNER_TYPE_ID  |  INTEGER  |  Тип владельца
TYPE_ID  |  INTEGER  |  Тип
PROVIDER_ID  |  TEXT  |  ID провайдера
PROVIDER_TYPE_ID  |  TEXT  |  Тип провайдера
PROVIDER_GROUP_ID  |  TEXT  |  Тип коннектора
ASSOCIATED_ENTITY_ID  |  INTEGER  |  ID связанной с делом сущности
SUBJECT  |  TEXT  |  Тема
CREATED  |  TIMESTAMP  |  Дата создания
LAST_UPDATED  |  TIMESTAMP  |  Дата изменения
START_TIME  |  TIMESTAMP  |  Начало
END_TIME  |  TIMESTAMP  |  Срок
DEADLINE  |  TIMESTAMP  |  Срок исполнения
COMPLETED  |  BOOLEAN  |  Выполнено
STATUS  |  TEXT  |  Статус
RESPONSIBLE_ID  |  INTEGER  |  Ответственный
PRIORITY  |  INTEGER  |  Важность
NOTIFY_TYPE  |  INTEGER  |  Тип уведомлений
NOTIFY_VALUE  |  INTEGER  |  Параметр уведомления
DESCRIPTION  |  TEXT  |  Описание
DESCRIPTION_TYPE  |  INTEGER  |  Тип описания
DIRECTION  |  INTEGER  |  Направление
LOCATION  |  TEXT  |  Место
ORIGINATOR_ID  |  TEXT  |  Внешний источник
ORIGIN_ID  |  TEXT  |  Внешний код
AUTHOR_ID  |  INTEGER  |  Создал
EDITOR_ID  |  INTEGER  |  Изменил
PROVIDER_DATA  |  TEXT  |  Данные провайдера
RESULT_MARK  |  INTEGER  |  RESULT_MARK
RESULT_VALUE  |  FLOAT8  |  RESULT_VALUE
RESULT_SUM  |  FLOAT8  |  RESULT_SUM
RESULT_CURRENCY_ID  |  TEXT  |  RESULT_CURRENCY_ID
RESULT_STATUS  |  INTEGER  |  RESULT_STATUS
RESULT_STREAM  |  INTEGER  |  RESULT_STREAM
RESULT_SOURCE_ID  |  TEXT  |  RESULT_SOURCE_ID
AUTOCOMPLETE_RULE  |  INTEGER  |  Автозаполнение


### bitrix_contacts
Контакты из битрикса

Колонка | Тип | Пояснение
--- | --- | ---
ID  |  INTEGER PRIMARY KEY NOT NULL  |  ID
POST  |  TEXT  |  Должность
COMMENTS  |  TEXT  |  Комментарий
HONORIFIC  |  TEXT  |  Обращение
NAME  |  TEXT  |  Имя
SECOND_NAME  |  TEXT  |  Отчество
LAST_NAME  |  TEXT  |  Фамилия
LEAD_ID  |  TEXT  |  Лид
TYPE_ID  |  TEXT  |  Тип контакта
SOURCE_ID  |  TEXT  |  Источник
SOURCE_DESCRIPTION  |  TEXT  |  Описание
COMPANY_ID  |  INTEGER  |  Компания
BIRTHDATE  |  DATE  |  Дата рождения
EXPORT  |  BOOLEAN  |  Участвует в экспорте контактов
HAS_PHONE  |  BOOLEAN  |  Задан телефон
HAS_EMAIL  |  BOOLEAN  |  Задан e-mail
HAS_IMOL  |  BOOLEAN  |  Задана открытая линия
DATE_CREATE  |  TIMESTAMP  |  Дата создания
DATE_MODIFY  |  TIMESTAMP  |  Дата изменения
ASSIGNED_BY_ID  |  INTEGER  |  Ответственный
CREATED_BY_ID  |  INTEGER  |  Кем создан
MODIFY_BY_ID  |  INTEGER  |  Кем изменен
OPENED  |  BOOLEAN  |  Доступен для всех
ORIGINATOR_ID  |  TEXT  |  Внешний источник
ORIGIN_ID  |  TEXT  |  Идентификатор элемента во внешнем источнике
ORIGIN_VERSION  |  TEXT  |  Версия оригинала
FACE_ID  |  TEXT  |  Привязка к лицам из модуля faceid
ADDRESS  |  TEXT  |  Адрес
ADDRESS_2  |  TEXT  |  Адрес (стр. 2)
ADDRESS_CITY  |  TEXT  |  Город
ADDRESS_POSTAL_CODE  |  TEXT  |  Почтовый индекс
ADDRESS_REGION  |  TEXT  |  Район
ADDRESS_PROVINCE  |  TEXT  |  Область
ADDRESS_COUNTRY  |  TEXT  |  Страна
ADDRESS_LOC_ADDR_ID  |  TEXT  |  Идентификатор адреса местоположения
UTM_SOURCE  |  TEXT  |  Рекламная система
UTM_MEDIUM  |  TEXT  |  Тип трафика
UTM_CAMPAIGN  |  TEXT  |  Обозначение рекламной кампании
UTM_CONTENT  |  TEXT  |  Содержание кампании
UTM_TERM  |  TEXT  |  Условие поиска кампании
UF_PIPEDRIVE_ID  |  TEXT  |  ID в Pipedrive
UF_TAG  |  TEXT  |  Метка
UF_DATE_CREATE  |  TIMESTAMP  |  Дата создания контакта
UF_LAST_TASK_DATE  |  TIMESTAMP  |  Дата последней задачи
UF_TITLE  |  TEXT  |  Роль
UF_LINKEDIN  |  TEXT  |  Linkedin
UF_CRM_1649758575330  |  TEXT  |  Описание контакта
UF_CRM_1649758723903  |  TEXT  |  Дополнительный телефон
UF_CRM_1649759373492  |  TEXT  |  Телефон 2
PHONE  |  TEXT  |  Телефон
EMAIL  |  TEXT  |  E-mail


### bitrix_stages_changes
Движения сделок по стадиям из битрикса

Колонка | Тип | Пояснение
--- | --- | ---
ID | INTEGER PRIMARY KEY NOT NULL | идентификатор записи
TYPE_ID | INTEGER | Тип записи. Может принимать значения: 1 - создание сущности, 2 - перевод на промежуточную стадию, 3 - перевод на финальную стадию
OWNER_ID | | INTEGER NOT NULL | Идентификатор сделки, в которой изменилась стадия
CREATED_TIME | TIMESTAMP | Дата и время попадания на стадию
RESPONSIBLE_ID | INTEGER |
CATEGORY_ID | INTEGER | Идентификатор направления (воронки)
STAGE_SEMANTIC_ID | TEXT | Семантика статуса (стадии). P - промежуточная стадия, S - успешная стадия, F - провальная стадия
STAGE_ID | TEXT | Идентификатор стадии

### bitrix_stages
Документация по сделкам из bitrix

Колонка | Тип                          | Пояснение
--- |------------------------------|--------------------------------
ID | INTEGER PRIMARY KEY NOT NULL | id сущности в битриксе
STAGE_ID	| STRING                       | Идентификатор стадии сделки
STAGE_NAME | STRING                       | Название стадии сделки
STAGE_ORDER_NR | INTEGER                      | Номер стадии внутри воронки
PIPELINE_ID | INTEGER                      | Идентификатор направления (воронки)
PIPELINE_NAME | TEXT                         | Название направления (воронки)
PIPEDRIVE_PIPELINE_ID	| INTEGER | Идентификатор воронки из pipedrive
SEMANTICS | TEXT                         | Семантика статуса (стадии). P - промежуточная стадия, S - успешная стадия, F - провальная стадия


### bitrix_time_in_stages
Время нахождения на стадиях стедлок из битрикса

Колонка | Тип | Пояснение
--- | --- | ---
deal_id | INTEGER | ID сделки
stage_id | TEXT | Идентификатор стадии
came_into_stage_time | TIMESTAMP | Время прихода на стадию
got_out_of_stage_time | TIMESTAMP | Время ухода со стадии
stay_duration_seconds | INTEGER | Время нахождения сделки на стадии в секундах

### bitrix_requisites
Реквизиты из битрикса, дока тут: https://dev.1c-bitrix.ru/rest_help/crm/requisite/requisite_fields.php
(Где-то вместо пояснения приведен пример значений поля)

Колонка | Тип                          | Пояснение
--- |------------------------------| ---
ID | INTEGER | ID
ENTITY_TYPE_ID | INTEGER | ID типа сущности
ENTITY_ID | INTEGER | ID сущности
PRESET_ID | INTEGER | ID пресета
DATE_CREATE | TIMESTAMP | Дата создания
DATE_MODIFY | TIMESTAMP | Дата изменения
CREATED_BY_ID | INTEGER | Создал
MODIFY_BY_ID | INTEGER | Изменил
NAME | TEXT | Название
CODE | TEXT | Код
XML_ID | TEXT | Внешний код
ORIGINATOR_ID | TEXT | ORIGINATOR_ID
ACTIVE | CHAR | Активен
ADDRESS_ONLY | CHAR | ADDRESS_ONLY
SORT | INTEGER | Сортировка
RQ_NAME | TEXT | Ф.И.О.
RQ_FIRST_NAME | TEXT | Имя
RQ_LAST_NAME | TEXT | Фамилия
RQ_SECOND_NAME | TEXT | Отчество
RQ_COMPANY_NAME | TEXT | Сокращенное наименование организации
RQ_COMPANY_FULL_NAME | TEXT | Полное наименование организации
RQ_COMPANY_REG_DATE | TEXT | Дата государственной регистрации
RQ_DIRECTOR | TEXT | Ген. директор
RQ_ACCOUNTANT | TEXT | Гл. бухгалтер
RQ_CEO_NAME | TEXT | RQ_CEO_NAME
RQ_CEO_WORK_POS | TEXT | RQ_CEO_WORK_POS
RQ_CONTACT | TEXT | Контактное лицо
RQ_EMAIL | TEXT | E-Mail
RQ_PHONE | TEXT | Телефон
RQ_FAX | TEXT | Факс
RQ_IDENT_DOC | TEXT | Вид документа
RQ_IDENT_DOC_SER | TEXT | серия
RQ_IDENT_DOC_NUM | TEXT | номер
RQ_IDENT_DOC_PERS_NUM | TEXT | RQ_IDENT_DOC_PERS_NUM
RQ_IDENT_DOC_DATE | TEXT | дата выдачи
RQ_IDENT_DOC_ISSUED_BY | TEXT | кем выдан
RQ_IDENT_DOC_DEP_CODE | TEXT | код подразделения
RQ_INN | TEXT | ИНН
RQ_KPP | TEXT | КПП
RQ_USRLE | TEXT | RQ_USRLE
RQ_IFNS | TEXT | ИФНС
RQ_OGRN | TEXT | ОГРН
RQ_OGRNIP | TEXT | ОГРНИП
RQ_OKPO | TEXT | ОКПО
RQ_OKTMO | TEXT | ОКТМО
RQ_OKVED | TEXT | ОКВЭД
RQ_EDRPOU | TEXT | RQ_EDRPOU
RQ_DRFO | TEXT | RQ_DRFO
RQ_KBE | TEXT | RQ_KBE
RQ_IIN | TEXT | RQ_IIN
RQ_BIN | TEXT | RQ_BIN
RQ_ST_CERT_SER | TEXT | Серия св. о гос. регистрации
RQ_ST_CERT_NUM | TEXT | Номер св. о гос. регистрации
RQ_ST_CERT_DATE | TEXT | Дата св. о гос. регистрации
RQ_VAT_PAYER | CHAR | RQ_VAT_PAYER
RQ_VAT_ID | TEXT | RQ_VAT_ID
RQ_VAT_CERT_SER | TEXT | RQ_VAT_CERT_SER
RQ_VAT_CERT_NUM | TEXT | RQ_VAT_CERT_NUM
RQ_VAT_CERT_DATE | TEXT | RQ_VAT_CERT_DATE
RQ_RESIDENCE_COUNTRY | TEXT | RQ_RESIDENCE_COUNTRY
RQ_BASE_DOC | TEXT | RQ_BASE_DOC


### bitrix_leads_distribution
Время нахождения на стадиях стелок из битрикса

Колонка | Тип | Пояснение
--- | --- | ---
id | INTEGER | ID распределения
dt  | DATE | дата
deal_id | INTEGER | ID сделки
rule | TEXT | правило, по которому произошло распределение
new_stage | TEXT | ID стейджа, на который отправилась сделка
new_owner | INTEGER | ID нового владельца сделки
probability_coefficient | FLOAT | коэффициент, которорый учитывался при распределении
distribution_deal_weight | FLOAT | вес сделки, который балансируется при распределени сделок между менеджерами (1/probability_coefficient)


### bitrix_tasks
Данные по задачам в битриксе

Колонка | Тип   | Пояснение
--- |-------|-----------
ID | INTEGER PRIMARY KEY NOT NULL | ID задачи
PARENT_ID | INTEGER | ID родительской задачи
TITLE | TEXT NOT NULL | Название задачи
DESCRIPTION | TEXT  | Описание задачи
GOOD_MARK | BOOLEAN | Оценка задачи (True, если положительная)
PRIORITY | TEXT  | Приоритет задачи
STATUS | TEXT  | Статус задачи
MULTITASK | BOOLEAN | Множественная задача
NOT_VIEWED | BOOLEAN | Не просмотрено
REPLICATE | BOOLEAN | Повторяемая задача
GROUP_ID | INTEGER | Проект
STAGE_ID | INTEGER | Стадия
CREATED_BY | INTEGER NOT NULL | Постановщик задачи
CREATED_DATE | TIMESTAMP | Дата создания задачи
RESPONSIBLE_ID | INTEGER NOT NULL | Исполнитель задачи
ACCOMPLICES | ARRAY | ACCOMPLICES
AUDITORS | ARRAY | Аудиторы
CHANGED_BY | INTEGER | Автор изменения задачи
CHANGED_DATE | TIMESTAMP | Дата и время изменения задачи
STATUS_CHANGED_BY | INTEGER | Автор изменения статуса задачи
STATUS_CHANGED_DATE | TIMESTAMP | Дата и время изменения статуса задачи
CLOSED_BY | INTEGER | Автор закрытия задачи
CLOSED_DATE | TIMESTAMP | Дата и время закрытия задачи
ACTIVITY_DATE | TIMESTAMP | Дата активности
DATE_START | TIMESTAMP | Дата начала
DEADLINE | TIMESTAMP | Крайний срок
START_DATE_PLAN | TIMESTAMP | Плановое начало
END_DATE_PLAN | TIMESTAMP | Плановое завершение
GUID | TEXT  | GUID
XML_ID | TEXT  | XML_ID
COMMENTS_COUNT | INTEGER | Количество комментариев
SERVICE_COMMENTS_COUNT | INTEGER | Количество сервисных комментариев
NEW_COMMENTS_COUNT | INTEGER | Количество новых комментариев
ALLOW_CHANGE_DEADLINE | BOOLEAN | Возможность изменения дедлайна
ALLOW_TIME_TRACKING | BOOLEAN | Возможность трекинга времени
TASK_CONTROL | BOOLEAN | Принять работу
ADD_IN_REPORT | BOOLEAN | Добавить отчет
FORKED_BY_TEMPLATE_ID | BOOLEAN | Создано из шаблона
TIME_ESTIMATE | INTEGER | Затраченное время
TIME_SPENT_IN_LOGS | INTEGER | Затраченое время из истории изменений
MATCH_WORK_TIME | BOOLEAN | Пропустить выходные дни
FORUM_TOPIC_ID | INTEGER | FORUM_TOPIC_ID
FORUM_ID | INTEGER | FORUM_ID
SITE_ID | TEXT  | SITE_ID
SUBORDINATE | BOOLEAN | Задача подчиненного
FAVORITE | BOOLEAN | FAVORITE
EXCHANGE_MODIFIED | TIMESTAMP | EXCHANGE_MODIFIED
EXCHANGE_ID | INTEGER | EXCHANGE_ID
OUTLOOK_VERSION | INTEGER | OUTLOOK_VERSION
VIEWED_DATE | TIMESTAMP | Дата последнего просмотра
SORTING | DOUBLE PRECISION | Индекс сортировки
DURATION_PLAN | INTEGER | Затрачено (план)
DURATION_FACT | INTEGER | Затрачено (фактически)
CHECKLIST | ARRAY | Чеклист
DURATION_TYPE | TEXT  | Единица измерения длительности
IS_MUTED | BOOLEAN | IS_MUTED
IS_PINNED | BOOLEAN | IS_PINNED
IS_PINNED_IN_GROUP | BOOLEAN | IS_PINNED_IN_GROUP
DESCRIPTION_IN_BBCODE | BOOLEAN | DESCRIPTION_IN_BBCODE
GROUP | ARRAY | GROUP

## spark_orgs_info
Данные по организациям из Спарка


Колонка | Тип | Пояснение
--- | --- | ---
spark_id | integer | Идентификатор компании в СПАРК
name | text | Наименование компании
main_okved2_code | text | ОКВЕД: код
main_okved2_name | text | ОКВЕД: наименование
ogrn | text | ОГРН
inn | text | ИНН
kpp | text | КПП
city | text | Юридический адрес: город
region | text | Юридический адрес: регион
leader_fio | text | Руководитель: ФИО
leader_position | text | Руководитель: должность
phone_list | text | Список телефонов через запятую
email | text | email
website | text | website
reg_date | date | Дата регистрации
population | integer | Последняя актуальная численность персонала по данным ФНС
revenue | double precision | Выручка, млн. рублей
last_update_date | date | Дата последнего обновления информации по организации
