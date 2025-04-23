## FreelancerBsRatingImportJob

### Продукт/подсистема

Фрилансеры в Директе.

Фрилансер - частный предприниматель, прошедший сертификацию в Яндексе на знание инструментов Директа и возмездно помогающий другим клиентам настраивать рекламные кампании в Директе.

<https://direct.yandex.ru/dna/freelancers/>


### Роль в работе продукта/подсистемы

ВыИмпортирует рейтинг фрилансеров, расчитанный по формулам ОКР. Этот рейтинг показывается только самим фрилансерам.


### Датафлоу

Рейтинг из [hahn.//home/bs/freelancers/direct/export](https://yt.yandex-team.ru/hahn/navigation?path=//home/bs/freelancers/direct/export) пишем в табличку [ppc.freelancers](https://direct-dev.yandex-team.ru/db/ppc/tables/freelancers.html) в колонки `adv_quality_rating` и `adv_quality_rank`. Данные готовят в ОКР скриптами из <https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/freelancer_ranking>


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateFreelancerRatingsJob.working.production)
- [Логи](https://nda.ya.ru/t/95YgIFVO3rF7zb)


### Какая функциональность пострадает от отказа джобы

- (некритично) Специалисты будут видеть неактуальный рейтинг своей эффективности, расчитанный Яндексом.


### Как пользователи (или команда) заметят проблему и через какое время

- Пользователи-фрилансеры могут заметить, что рейтинг перестал обновляться.


### Контакты разработчиков и менеджеров

Разработчики: [Максим Логунов](https://staff.yandex-team.ru/maxlog), [Роман Кухта](https://staff.yandex-team.ru/kuhtich)
Со стороны ОКР: [Алексей Поспелов](https://staff.yandex-team.ru/apos)


### Желательное время исправления в случае поломки

Неделя


### Способы регулирования работы джобы

—


### Известные причины поломок

—

### Дополнительно: тонкости и подводные камни

—
