## UpdateStoreContentJob

### Продукт/подсистема

Подсистема получения информации о мобильных приложениях, в основном для РМП кампаний (Реклама мобильных приложений).


### Роль в работе продукта/подсистемы

Обновление информации о мобильных приложениях в [ppc.mobile_content](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_content.html).


### Датафлоу

Раз в час проверяет нет ли приложений, которые не обновлялись уже сутки и запрашивает для них информацию из динамических таблиц, построенных джобой [MobileAppsSyncJob](MobileAppsSyncJob.md). Обновляет данные приложения клиентов в [ppc.mobile_content](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_content.html) сбрасывает статус синхронизации с БК (когда требуется).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateStoreContentJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'updatestorecontent.UpdateStoreContentJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будет обновляться информация о приложениях в [ppc.mobile_content](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_content.html).


### Как пользователи (или команда) заметят проблему и через какое время

Показ объявлений приложений, которые уже удалены со сторов?
Старые данные в объявлениях: рейтинг, иконка? (сейчас вроде строится прямой канал Аврора->CaeSaR).


### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Игорь Гердлер](https://staff.yandex-team.ru/gerdler)


### Желательное время исправления в случае поломки

1 - 2 дня.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
