## Расследование проблем с подпиской

Основные шаги:
- проанализировать [график](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_prod/) триггеров на предмет аномального роста одного или нескольких триггеров
- помним, что подписку генерирует не только piper, но и scanner со stroller (для их анализа можно использовать [кастомный фильтр сигналов yasm](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiperwhite;ctype=prestable,production;prj=market;hosts=ASEARCH;graphs=%7Bunistat-mdm_subscriber_*_dmmm%7D/))
- проверить была ли отправка в сервис подписки можно через [logfeller](https://yql.yandex-team.ru/Operations/Yh44nVZ1O89BrwOB8iOIOJbaFTAWYUGVHMvWAK4g8L0=) по business_id, offer_id.
- матчим аномалии с временем первого проблемного события
- найдя часто меняющееся поле, можно [сравнить](https://yql.yandex-team.ru/Operations/YfA0ngVK8KlC1WYmyQJAbjz_yVVTKaBhtUgxEPPdkns=) содержимое топиков подписчика с бекапами хранилища на предмет качественного изменения полей внутри этого поля
- для поиска аномалий в качественном изменении полей подписки можно использовать [группировку](https://yql.yandex-team.ru/Operations/YfA7LAVK8KlC1WpEmojDtMsL5rdsa8nb_f6DAPMPpmk=)
