### Продукт/подсистема

Превью оферов для еком доменов

### Роль в работе продукта/подсистемы

Удаляет из MBI сайты для превью, ранее отправленные джобой `SendEcomDomainToMBIJob`, но удаленные из таблицы `ppcdict.ecom_domains` в Директе

### Датафлоу

- Находит yql-запросом все записи из выгрузки таблицы `shops_web.direct_site_preview` (`//home/market/production/mbi/dictionaries/direct_site_preview`) маркетные id (`partner_id` и `feed_id`) которых отсутствуют в `ppcdict.ecom_domains`
- Отправляет найденные id в MBI (`/direct/site/delete-preview`) для их удаления из таблицы `shops_web.direct_site_preview`

### Способы наблюдения за текущим состоянием
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.DeleteSitePreviewsFromMBIJob.working.production)
- [Логи](https://direct.yandex.ru/logviewer/short/sdpUYxPf4fcso5)
- [Solomon мониторинги](https://nda.ya.ru/t/sQKgGOAs4aVMaA) - графики отображающие количество еком доменов в разных статусах

### Какая функциональность пострадает от отказа джобы

Перестанут удаляться сайты для превью в MBI, из-за чего их количество может достигнуть лимита, и в следствии в джобе `SendEcomDomainToMBIJob` будут возникать ошибки о превышении допустимого количества сайтов для превью.

### Как пользователи (или команда) заметят проблему и через какое время

Новые сайты для превью в MBI перестанут появляться, а следовательно отправляться в Самовар и оффера перестанут приходить (`ReceiveEcomDomainsPreviewsJob`), из-за чего не будет формироваться превью

### Контакты разработчиков и менеджеров

Разработчики: [Дмитрий Анощенков](https://staff.yandex-team.ru/dmitanosh) <br/>
Менеджеры: [Дмитрий Уляшев](https://staff.yandex-team.ru/ulyashevda)

### Желательное время исправления в случае поломки

В течение суток

### Способы регулирования работы джобы


### Известные причины поломок

Недоступны hahn и arnold - в логах ошибки выполнения YQL запроса

### Дополнительно: тонкости и подводные камни
