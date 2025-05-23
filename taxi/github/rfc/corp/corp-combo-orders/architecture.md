# Массовый развоз
https://st.yandex-team.ru/CORPDEV-2596

Проблема: клиенты хотят массово заказывать такси своим сотрудникам, например ночью заканчивается
смена, из КК заказывают машины на 30 человек по домам. Сейчас это крайне неудобно, потому что
вбивать все эти поездки клиенту нужно по очереди, "оптимальность" маршрутов клиент пытается 
подобрать сам вручную.

Если коротко, то суть задачи в том, чтобы у клиента появилась возможность вбивать на фронте 
набор сотрудников и адресов, мы должны разделить этих сотрудников на машины так, чтобы 
маршруты каждого заказа были наиболее "оптимальными". Далее у клиента должна быть возможность
создать такие массовые (с несколькими пассажирами в одной машине) заказы.

### Архитектура

Наброски в miro: https://miro.com/welcomeonboard/WTU4eVd6RDhXcndYM0xPZ1BMWFU2VDI4Y2c5MmhrVmNjUlRHam5pTjVQTWNOY1VuODFHRFlLNzBQaDFnZkZuTnwzMDc0NDU3MzYyNDQzOTMxMDg0

И картинкой оттуда:

![alt text](https://jing.yandex-team.ru/files/egorgr/Screenshot%202021-08-26%20at%2015.11.38.png)

#### Описание того, что изображено на диаграмме

corp-mass-orders - новый сервис (выделен красным). Кажется, что он необходим, потому что не хочется
такой большой логикой еще отягощать taxi-corp и монгу. По поводу нейминга пока придумывались такие 
варианты: corp-mass-orders, corp-combo-orders.

Примерный флоу работы массового развоза:

1)  Фронт делает запрос на генерацию оптимальных маршрутов. Отправляет телефоны сотрудников и адреса.
Кажется тут два варианта:

    a) Фронт идет сначала в taxi-corp. Тут taxi-corp проксирует это в corp-mass-orders. 
    corp-mass-orders ставит таску в сервисе маршрутизации, запоминает инфу о ней в базе. 

    b) Либо все то же самое, только без taxi-corp. Здесь не очень хочется
    ходить через taxi-corp, может стоит подумать о том, как обойтись без него (auth proxy?)

2)  Фронт периодически полит это (в той же ручке с тем же токеном идемпотентности или же в отдельной 
ручке по task_id). 

3)  Фронт получил оптимальные маршруты, у клиента есть возможность что-то подредачить. После этого
идет запрос на создание массового заказа. Тут кажется есть два варианта:

    a) Запрос должен дойти в corp-mass-orders (через taxi-corp или нет), чтобы сразу
    сохранить информацию о создании заказа в базу corp-mass-orders. Сам заказ можно сделать 
    запросом с TVM в taxi-corp (как сейчас работает sber-int-api).

    b) Возможно, здесь и не нужно идти через corp-mass-orders и можно сразу просто создать заказ
    в taxi-corp. Инфу о заказах в corp-mass-orders кажется можно будет получать из ProcaaS.
    
    Реализовывать свою логика заказа в corp-mass-orders кажется не нужно, не хочется копипастить 
    логику из taxi-corp, да и в этой логике сильно завязана монга. 
   
4)  При создании массового заказа taxi-corp в запросе на создание драфта в протокол должен будет 
проставить какой нибудь доп тег (отметка массового развоза) и/или список user_ids. 

5)  Протокол соответственно должен прорастить эти поля в order_proc. Похожее текущему и предыдущему 
пункту было недавно проделано с новыми центрами затрат.

6)  Еще некоторые сложности, связанные с предыдущими двумя пунктами:

    - taxi-corp и протокол ходят в /corp_paymentmethods. Тут обсуждалось, 
    что при массовом развозе лимиты сотрудников проверяться не должны. Наверное тут надо сделать 
    доработки, чтобы taxi-corp и протокол слали какой то флаг и/или user_ids при массовом развозе, 
    а  /corp_paymentmethods при наличии этого флага проверял только клиентские чекеры. 
    Либо же вообще можно сделать новую ручку в corp-int-api, которая будет проверять 
    клиентские чекеры и существование всех сотрудников в базе.
    
    - кто непосредственный пассажир (owner поездки)? Были мысли, что это может быть кто-то из
    реальных пассажиров (например последний в маршруте). Тут надо подумать и над тем, 
    как это все должно отображаться в реестрах.

7)  В py-2 по наличию новых полей в order_proc мы сможем понять, что поездка массовая. При массовой
поездке траты будем начислять только на департаменты. 

    Здесь есть вопрос, что если в одну поездку попадут люди из разных департаментов? 
Как писать траты? Разделять между департаментами выглядит не очень, думаем над тем, чтобы не 
сажать в одну машину таких пассажиров.

8)  Кажется, что можно подписаться на события изменений заказа в ProcaaS. Для этого нужно 
завести STQ в corp-mass-orders, которая будет сохранять изменения в базу. Также в этой stq можно
будет перезаказывать такси в рамках какого то временного интервала, если оно не нашлось 
или водитель отказался от поездки. 

    Еще тут можно будет слать какие-нибудь смс пассажирам. Смски сейчас шлются в py-2, но кажется 
переезжают в какой-то микросервис, может получится его заиспользовать?

9)  Для реестров, истории поездок и всего такого для массовых поездок кажется, что все основное
так же останется в taxi-corp (corp-reports для отчетов). В монге в corp_orders эти заказы тоже будут,
так что это все по сути должно заработать без сильных изменений. 

    Можно будет сделать какие-то ручки получения информации о заказах в corp-mass-orders, если будет 
какая-нибудь страница для отображения только этих заказов. 

#### Что смущает
-   если ходить в corp-mass-orders через taxi-corp, то для создания заказа (если будем создавать его
проходя через corp-mass-orders) мы будем слать запросы taxi-corp -> corp-mass-orders -> taxi-corp.
Это выглядит как-то сомнительно. 
    
    Вообще в голову приходят мысли о том, что было круто вынести все, что связано с обычными 
заказами в отдельный сервис. Может даже не в новый, а в corp-orders (название подходящее и там 
хранятся заказы еды и драйва), но кажется сделать это сложновато.

-   вся эта история с тем, что из всех пассажиров выбирается какой-то один, на кого фактически 
вешается поездка выглядит как-то костыльно. У такого пассажира поездка будет в истории в приложении,
у остальных нет. Ну и всякие остальные моменты с смсками, уведомлениями, реестрами.
