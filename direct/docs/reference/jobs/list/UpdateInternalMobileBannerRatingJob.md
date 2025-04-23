## UpdateInternalMobileBannerRatingJob

### Продукт/подсистема

[Внутренняя реклама (aka Банана)](../../../glossary/glossary.md#internal-ads).


### Роль в работе продукта/подсистемы

Обновление рейтинга рекламируемых мобильных приложений Яндекса (баннеров внутренней рекламы с шаблоном `3103`).
Рейтинг приложений меняется в Google Play и AppStore и нам нужно обновлять эти значения для баннеров рекламы мобильных приложений.


### Датафлоу

- Выгружаются из таблицы [banners_internal](https://direct-dev.yandex-team.ru/db/ppc/tables/banners_internal.html) текущие значения рейтинга (`template_variables -> json`, поле `rating`) для всех показываемых, неархивных баннеров на шарде с `template_id = 3103`.
- Выгружаются актуальные значения рейтинга из [//home/direct/extdata-mobile/gplay/latest](https://yt.yandex-team.ru/seneca-vla/navigation?offsetMode=key&path=//home/direct/extdata-mobile/gplay/latest) и [//home/direct/extdata-mobile/itunes/latest](https://yt.yandex-team.ru/seneca-vla/navigation?offsetMode=key&path=//home/direct/extdata-mobile/itunes/latest) по url, указанным в обновляемых баннерах.
- Обновляются `template_variables` для тех баннеров, значения рейтинга которых изменились.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateInternalMobileBannerRatingJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'internal.UpdateInternalMobileBannerRatingJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Рейтинг рекламируемых мобильных приложений перестанет обновляться.


### Как пользователи (или команда) заметят проблему и через какое время

- Пользователи (не Директа), которые увидят баннер, будут видеть неактуальный рейтинг.
- Наши маркетологи увидят неактуальный рейтинг в интерфейсе Директа (не совпадающий с Google play и AppStore).


### Контакты разработчиков и менеджеров

Разработчики: [Бехруз Афзали](https://staff.yandex-team.ru/xy6er), [Дмитрий Анощенков](https://staff.yandex-team.ru/dmitanosh) <br/>
Менеджеры: [Иван Пахомов](https://staff.yandex-team.ru/irpakhomov), [Марина Ежова (Баитова)](https://staff.yandex-team.ru/ezhova-m)


### Желательное время исправления в случае поломки

В течении суток.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

