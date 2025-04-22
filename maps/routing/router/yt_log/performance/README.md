[Тасклет](https://wiki.yandex-team.ru/users/workfork/tasklety/) для расчета производительности роутера. 
<br><br><br>
Работает это примерно так:
<br>[Sandbox task](https://sandbox.yandex-team.ru/scheduler/16945/view) запускается в 5 утра каждый день. 
Рассчет производится на основе логов, залитых на [YT](yt.yandex-team.ru/hahn/navigation?path=//logs/maps-router-log/1d)(поэтому важно чтобы к моменту старта таски появилась таблица), а результат заливается в [stat](https://stat.yandex-team.ru/Maps_Plus_Beta/AutomotiveRouter/performance?scale=d&tvm_id=_in_table_&request=%2Fv2%2Froute&_period_distance=1&_incl_fields=avr&_incl_fields=quant_99&_incl_fields=quant_95&_incl_fields=quant_90&_incl_fields=quant_50&_incl_fields=count).
Затем, на основе этих данных строятся графики, которые находятся тут https://wiki.yandex-team.ru/users/alekseev-a-v/Router-Performance/
<br><br><br>

Как  поправить таску: 
 - Поправьте код
 - Проверьте правильность выполнения с помощью команды ya make && ./performance run Performance  --input '{}' --local
   . При этом необходимо передать YQL-token и пароль для робота(можно найти у [abc:maps-core-driving-router](https://abc.yandex-team.ru/services/maps-core-driving-router/)), т.к. локально нет секретницы. 
 - [этот пункт не актуален пока не подключена секретница]Уберите свои токены. Выполните ya make && ./performance run Performance  --input '{}' --sandbox. Задача должно отработать
 - В результате предыдущей команды создалась сэндбокс таска и ресурс. Необходимо перейти в ресурс и нажать important - это выставит ttl в inf. 
 - Затем надо перейти в [Sandbox task](https://sandbox.yandex-team.ru/scheduler/16945/view) и отредактировать - во вкладке Advanced указать бинарный ресурс из предыдущего шага
<br><br><br>

Todo list:
 - добавить секретницу, подсмотреть можно тут https://a.yandex-team.ru/review/846029/files/2#file-21906710
 - разобраться, как избавиться от лишних протобуфных полей
 - перейти на 3ий питон по закрытию https://st.yandex-team.ru/TASKLET-32
 - разобраться со статусом таски: сейчас она завершается успехом, даже если есть необработанное исключение
