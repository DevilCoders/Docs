#Логирование JS ошибок
Используем 34 счетчик метрики(доступен для просмотра суперридерам) 
https://metrika.yandex.ru/stat/58dd0ff64b553c0f300d9154?period=week&id=34

Клиентские ошибки отправляем через «Параметры визитов» 
https://yandex.ru/support/metrika/data/visit-params.xml
В отчете:
https://jing.yandex-team.ru/files/skywhale/2017-03-28%2020-00-09.png
https://jing.yandex-team.ru/files/skywhale/2017-03-28%2020-05-14.png

Переписка про логирование 
https://ml.yandex-team.ru/thread/2370000003663069514/
Формат отправляемого запроса взят из Новостей
https://github.yandex-team.ru/news/nerpa/blob/dev/core/common.blocks/b-statcounter/__error-logger/b-statcounter__error-logger.js

Почему отправляем на прямую `https://mc.yandex.ru/watch/`, хотя в доке метрики(ссылка выше) указано, что отправлять параметры необходимо через специальные методы?
Мы стараемся не зависит от кода метрики то просто подсмотрели куда хотят эти методы.
Сам урл https://mc.yandex.ru/watch/' + counter + '/ не поменяется, а вот передаваемый параметр site-info
может измениться, если такое произойдет мы увидим в отчете, что к нам перестали приходить данные по ошибкам.

###Автор
[skywhale](https://staff.yandex-team.ru/skywhale)


