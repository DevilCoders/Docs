## Форма

Самый простой способ стрелять по `saas` - с помощью формы:  
https://ssm.n.yandex-team.ru/shoot_to_service

### Notes:
1. Патроны заливаются в виде `ID` в sandbox  
   ```
   ya upload --sandbox ~/Desktop/ammo.txt  
   Created resource id is 2339852532  
   ```
   В форму нужно писать только `ID` ресурса.
1. Список локаций передается через запятую, например `sas, vla`
1. target rps указывается из расчета на одну локацию.  
   Это суммарный `RPS` до которого таска будет грузить.  
   Если столько трафика уже есть в локации, доливать она не будет.
1. Во избежание проблем с cross-dc стрельбы по локациям проводятся последовательно.

### Пример стрельбы
Стрельба  
https://sandbox.yandex-team.ru/task/1044746768/view  
Создает дочерние таски на стрельбы по отдельным ДЦ:  
https://sandbox.yandex-team.ru/task/1044746768/children  
Внутри этих тасок есть ссылки на лунапарк:  
https://lunapark.yandex-team.ru/2816337  
https://lunapark.yandex-team.ru/2816325  
К родительскому тикету автоматически линкуются ссылки на мониторинги бекендов `saas`.

### Пример патронов
```
[X-Ya-Service-Ticket: 3:serv:...zQ]
/?service=vasgen_search_lb&dbgrlv=da&fsgta=_JsonFactors&snip=diqm%3D1&timeout=5000000&pron=pruncount500&kps=1&relev=all_factors;calc%3Doffer_time_diff:clamp(diff(1628447070,%23f_f_offer_publish_date_g),0,2592000);calc%3Df_publish_date_diff:diff(1628447070,%23f_f_offer_publish_date_g);calc%3Df_activate_date_diff:diff(1628447070,%23f_f_offer_activate_date_g);calc%3Df_publish_date_normed:mul(%23f_publish_date_diff,+0.0000003858);calc%3Df_activate_date_normed:clamp(%23f_activate_date_diff,+0,+2592000);calc%3Dsort_hash:fnvhash_f32(zdocid_i64());formula%3Dpruning&gta=_snippet_g&ms=proto&relev=enable_softness;attr_limit%3D100000000&text=%D0%B8%D1%89%D1%83%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%83%20%D0%B4%D0%BB%D1%8F%20%D0%B6%D0%B5%D0%BD%D1%89%D0%B8%D0%BD%20%D0%B2%20%D0%BD%D0%BE%D0%B2%D0%BE%D1%81%D0%B8%D0%B1%D0%B8%D1%80%D1%81%D0%BA%D0%B5&template=%25request%25+%3C%3C+i_epoch:%3E%3D%2217%22+%3C%3C+(s_offer_category_all_g:%22rabota_UR05lf%22)+%3C%3C+(s_offer_region_g:%22213%22)&p=0&numdoc=35
/?service=vasgen_search_lb&dbgrlv=da&fsgta=_JsonFactors&snip=diqm%3D1&timeout=5000000&pron=pruncount500&kps=1&relev=all_factors;calc%3Doffer_time_diff:clamp(diff(1628447070,%23f_f_offer_publish_date_g),0,2592000);calc%3Df_publish_date_diff:diff(1628447070,%23f_f_offer_publish_date_g);calc%3Df_activate_date_diff:diff(1628447070,%23f_f_offer_activate_date_g);calc%3Df_publish_date_normed:mul(%23f_publish_date_diff,+0.0000003858);calc%3Df_activate_date_normed:clamp(%23f_activate_date_diff,+0,+2592000);calc%3Dsort_hash:fnvhash_f32(zdocid_i64());formula%3Dpruning&gta=_snippet_g&ms=proto&relev=enable_softness;attr_limit%3D100000000&text=%D0%B8%D1%89%D1%83%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%83%20%D0%B2%20%D0%BD%D0%BE%D0%B2%D0%BE%D1%81%D0%B8%D0%B1%D0%B8%D1%80%D1%81%D0%BA%D0%B5&template=%25request%25+%3C%3C+i_epoch:%3E%3D%2217%22+%3C%3C+(s_offer_category_all_g:%22rabota_UR05lf%22)+%3C%3C+(s_offer_region_g:%22213%22)&p=0&numdoc=35
```
Текст запроса (в поле `text=`) должен быть url encoded.  
Сгенерировать tvm-тикет можно командой:
```
ya tool tvmknife get_service_ticket sshkey -s 2022096 -d 2011468
```
`tvm_id` для `source` и `destination` можно узнать распарсив какой-нибудь тикет из старых стрельб:
```
ya tool tvmknife parse_ticket 3:serv:AWD...5uPyXfiNCvLg
```
