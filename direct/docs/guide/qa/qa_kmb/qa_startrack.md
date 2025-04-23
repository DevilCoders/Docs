# Настройка трекера

Вся работа ведется в Стартреке: [https://st.yandex-team.ru](https://st.yandex-team.ru) <br>
Для удобства работы и мониторинга тикетов рекомендуется создать дашборд.
1) Вкладка Dashboards -> Create Dashboard

    {% cut "Скриншот" %}

    ![alt text](https://jing.yandex-team.ru/files/sudar/29-07-21__19-29-47.png "Скриншот")

    {% endcut %}

2)  заполнить название дашборда и выбрать вид расположения виджетов

    {% cut "Скриншот" %}

    ![alt text](https://jing.yandex-team.ru/files/sudar/29-07-21__19-41-15.png "Скриншот")

    {% endcut %}

3) добавить новый виджет с типом Issues

4) Рекомендую добавить 4 виджета: 
* Задачи, которые ждут тестирования от меня и тестируются<br>
Пример запроса: `QA-Engineer: me() AND Status: "Ready For Test", "Testing", "Need Info", "Need Improvement"` 

    {% cut "Пример" %}

    ![alt text](https://jing.yandex-team.ru/files/sudar/30-07-21__10-31-52.png "Пример")

    {% endcut %}
    
* Задачи, которые попали в релиз<br>
Пример запроса: `Tags: "release_testing" AND QA-Engineer: me() AND Status: !Closed `

    {% cut "Пример" %}

    ![alt text](https://jing.yandex-team.ru/files/sudar/29-07-21__20-01-36.png "Пример")

    {% endcut %}
    
* Задачи, назначенные на меня<br>
Пример запроса: `Assignee: me() AND Status: !Closed` 

    {% cut "Пример" %}

    ![alt text](https://jing.yandex-team.ru/files/sudar/29-07-21__20-34-25.png "Пример")

    {% endcut %}
    
* Задачи, ждущие ответа меня<br>
Пример запроса: `"Pending Reply From": me()  AND Status: !Closed` 

    {% cut "Пример" %}

    ![alt text](https://jing.yandex-team.ru/files/sudar/29-07-21__20-35-51.png "Пример")

    {% endcut %}


--
<br>
В случае неактуальности информации на данной странице можно обращаться к [Олегу Судареву](https://staff.yandex-team.ru/sudar)
