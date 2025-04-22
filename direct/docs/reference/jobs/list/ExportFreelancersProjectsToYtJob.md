## ExportFreelancersProjectsToYtJob

### Продукт/подсистема

Фрилансеры в Директе.

Фрилансер - частный предприниматель, прошедший сертификацию в Яндексе на знание инструментов Директа и возмездно помогающий другим клиентам настраивать рекламные кампании в Директе.

<https://direct.yandex.ru/dna/freelancers/>


### Роль в работе продукта/подсистемы

Выгружает связи между фрилансерами и их клиентами для ОКР и КД.


### Датафлоу

Выгружает записи из таблицы [ppc.freelancers_projects](https://direct-dev.yandex-team.ru/db/ppc/tables/freelancers_projects.html) в таблицу в YT [//home/direct/export/freelancers/freelancers_projects](https://yt.yandex-team.ru/arnold/navigation?offsetMode=key&path=//home/direct/export/freelancers/freelancers_projects) на кластеры hahn и arnold.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ExportFreelancersProjectsToYtJob.working.production)
- [Логи](https://nda.ya.ru/t/Ms4H87xS3rF6DF)


### Какая функциональность пострадает от отказа джобы

- (некритично) Данные используются для дашбордов КД (тут: <https://a.yandex-team.ru/arc/trunk/arcadia/client_analytics/freelance_info?rev=r7954506>)
- (некритично) Выгружаемые данные используются при расчёте ОКР-ного рейтинга, который мы потом забираем джобой `FreelancerBsRatingImportJob`


### Как пользователи (или команда) заметят проблему и через какое время

- Пожалуются из КД, когда заметят, что дашборды не обновляются.

### Контакты разработчиков и менеджеров

Разработчики: [Максим Логунов](https://staff.yandex-team.ru/maxlog), [Роман Кухта](https://staff.yandex-team.ru/kuhtich)


### Желательное время исправления в случае поломки

Неделя


### Способы регулирования работы джобы

—


### Известные причины поломок

—

### Дополнительно: тонкости и подводные камни

—
