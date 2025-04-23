# Описание сегментов для опросов CRM SPACE


### [Nirvana](https://nirvana.yandex-team.ru/flow/736f0cd9-5e54-43b6-a624-a28793099537/675e8f8e-a176-4688-b96d-677d22d92d6f/graph)

### Сегменты
| id                | Название в дашборде | Группа      | Slug                   | Воронки                   | Статусы  | Резолюции                                                                                           | Интервал времени            | Прочие условия                                 |
|-------------------|---------------------|-------------|------------------------|---------------------------|----------|-----------------------------------------------------------------------------------------------------|-----------------------------|------------------------------------------------|
| segment_2_space   | 2 Не купили (ТМ)    | Привлечение | D9fJmnfUAKvDpHQbshbKx6 | SMB: Cold Sales, SMB: GEO | Отказ    | Нет денег, Реклама не нужна, Не озвучил причину, Будет запускать но позже, Негативный опыт, Другое. | 1 день от перехода в статус | - Наличие откруток за посл. 12 месяцев: Искл.; |
| segment_2_1_space | 2_1 Успешно 1d      | Привлечение | GYtR9ywMjQw3NyDueHwgM8 | SMB: Cold Sales, SMB: GEO | Закрыт   | Решен                                                                                               | 1 день от перехода в статус |                                                |
|                   |                     |             |                        |                           |          |                                                                                                     |                             |                                                |


### Про данные
Основной таблицей, для фомирования сегментов является таблица [issues_view_table](https://yt.yandex-team.ru/hahn/navigation?path=//home/smbsales/public/issues_view_table)
(её [документация](https://wiki.yandex-team.ru/sales/massales/okoreports/opisanie-nashix-istochnikov/descriptionissueview/)
и [код](https://a.yandex-team.ru/arcadia/smbsales/regular_jobs/issue_view_new2021.sql)).
