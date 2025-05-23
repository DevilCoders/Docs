## FreelancerCardReceivingJob

### Продукт/подсистема

Фрилансеры в Директе.

Фрилансер - частный предприниматель, прошедший сертификацию в Яндексе на знание инструментов Директа и возмездно помогающий другим клиентам настраивать рекламные кампании в Директе.

Карточка фрилансера - информация о фрилансере, содержащая его самоописание, фотографию и контактные данные. Карточка фрилансера не может изменяться после прохождения модерации, может быть создана только новая версия.


### Роль в работе продукта/подсистемы

Получает результаты модерации карточек фрилансеров и в случае "ОК" публикует прошедшую модерацию новую версию карточки фрилансера.


### Датафлоу

- Получает результаты модерации из топика `modadvert-sm-direct-results-log` (владелец: Группа разработки модерации рекламы)
- Проставляет соответствующие статусы карточкам фрилансеров в таблице: [ppc.freelancers_card](https://direct-dev.yandex-team.ru/db/ppc/tables/freelancers_card.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.FreelancerCardReceivingJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'service~'method~'span_id~'message)~conditions~(service~'direct.jobs~method~'receiving.FreelancerCardReceivingJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Перестанут публиковаться новые версии карточек фрилансеров.


### Как пользователи (или команда) заметят проблему и через какое время

Фрилансеры будут редактировать информацию о себе, но она так и не будет появляться в описании фрилансера для других пользователей.


### Контакты разработчиков и менеджеров

Разработчики: [Антон Тухватулин](https://staff.yandex-team.ru/ajkon), [Максим Логунов](https://staff.yandex-team.ru/maxlog)


### Желательное время исправления в случае поломки

Часы, возможно день. Фрилансеров мало (десятки), но в случае поломки джобы у них пропадёт возможность поменять своё описание или фотографию на сайте Директа.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
