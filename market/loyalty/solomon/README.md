
# Обновление алертов в Solomon

Solomon это система мониторингов. Настройки Loyalty в этой системе находятся по адресу 
https://solomon.yandex-team.ru/admin/projects/market-loyalty/. 

Непосредстенно графики можно посмотреть по 
адресу https://solomon.yandex-team.ru/?project=market-loyalty

Поставщиком данных для мониторингов является
clickphite который мы конфигурируем через market-health

```git clone git@github.yandex-team.ru:market-infra/market-health.git``` 

### Про Solomon
Solomon получает данные от Clickphite и строит по этим данным графики. Значения которые 
приезжают в Solomon в его терминологии называются сенсорами. Над сенсорами можно определять 
мониторинги которые в терминологии Solomon называются алертами.

Алерт это предикат который вычисляется над сенсором раз в одну минуту. Берется ряд точек в заданом
временном окне (например 5 минут) и к этим точкам применяется какая нибудь агрегирующая функция. 
Простейшие функции: минимальное значение (min), максимальное значение (max), среднее значение (avg).
Полученное значение сравнивается с пороговым значением и если оно выходит за него то алерт переходит 
в состояние ALARM, иначе остается в состоянии OK. Кроме этих состояний есть еще другие состояния
о которых можно почитать в доке.

С алертом можно связать канал. Каналы нужны чтобы отправлять состояния алертов другие системы. 
Мы отправляем состояния алертов в Juggler.

Руководство пользователя можно найти в Вики: https://wiki.yandex-team.ru/Solomon/userguide/

### Скипты
#### script.py
Дергает ручку [/health/alerts](
http://market-loyalty.tst.vs.market.yandex.net:35815/swagger-ui.html#/page-matcher-controller/getRequestMappingHealthParamsUsingGET) на
localhost:8080 и пушит алерты в Solomon. Если алерты поменялись то обновляет, если алерты новые то 
добавляет. Удалять не умеет.

Логично что перед тем как запускать нужно запустить локально бекенд лоялти.

#### delete.py
Удаляет все алерты id которых начинается с '-'.