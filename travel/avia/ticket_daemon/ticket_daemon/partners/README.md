# Модуль опроса партнера

## Интерфейс

### Обязательные

Эти методы обязательны для реализаци в модуле.
Без них модуль некорректен.

```python
@QueryTracker.init_query
def query(tracker, q):
    """
    Опрашивает парнера, возвращает варианты.

    Parameters
    ----------
    tracker : travel.avia.ticket_daemon.ticket_daemon.lib.tracker.QueryTracker
        
    q : travel.avia.ticket_daemon.api.Query
        Параметры запроса.

    Returns
    -------
    Iterable[Iterable[travel.avia.ticket_daemon.ticket_daemon.api.flights.Variant]]
        Варианты перелета.
    """
```

### Опциональные

Для данных методов есть реализации по умолчанию.
Прописывать их нужно в случае необходимости кастомных сценариев.

```python
def book(order_data):
    """
    Возвращает данные для перенаправления на страницу партнера с вариантом.
    Далее на результат навешивается marker и yaclid.

    Parameters
    ----------
    order_data : dict
        Данные заказа для генерации ссылки перехода.

    Returns
    -------
    dict
        Данные для перехода.
        Допустимые поля: url, m_url, post_data, marker
    """
```

```python
def generate_marker():
    """
    Генерирует кастомный маркер для URL.

    Returns
    -------
    str
        Маркер.
    """
```

```python
def add_marker_to_url(marker_field_name, marker_value, url):
    """
    Генерирует кастомный маркер для URL.

    Parameters
    ----------
    marker_field_name : str
        Имя элемента query url.
    
    marker_value : str
        Значение маркера.
    
    url : str
        url, к которому нужно добавить маркер.

    Returns
    -------
    str
        url, к которому было добалвено значение маркера.
    """
```

## Удаленные модули

| Название модуля           | Коммит        | Тикет создания              |
|---------------------------|---------------|-----------------------------|
| aeroflot.py               | [Ссылка][1]   | [RASPTICKETS-8841][t1]      |
| aeroflot2.py              | [Ссылка][2]   | [RASPTICKETS-19097][t2]     |
| aeroflot2_white_monday.py | [Ссылка][3]   | [RASPTICKETS-19097][t2]     |
| aeroflot3.py              | [Ссылка][4]   | [RASPTICKETS-19097][t2]     |
| aeroflot3_plus.py         | [Ссылка][5]   | [RASPTICKETS-19097][t2]     |
| aeroflot3_plus_ru.py      | [Ссылка][6]   | [RASPTICKETS-19097][t2]     |
| aeroflot3_ru.py           | [Ссылка][7]   | [RASPTICKETS-19097][t2]     |
| amargo2.py                | [Ссылка][8]   |                             |
| aviakass4.py              | [Ссылка][9]   | [RASPTICKETS-8706][t3]      |
| ctrip.py                  | [Ссылка][10]  | [RASPTICKETS-10011][t4]     |
| ctrip2.py                 | [Ссылка][11]  | [RASPTICKETS-16467][t5]     |
| expressavia3.py           | [Ссылка][12]  | [RASPTICKETS-10266][t6]     |
| gotogate.py               | [Ссылка][13]  | [RASPTICKETS-16303][t7]     |
| ozon.py                   | [Ссылка][14]  |                             |
| pobeda2.py                | [Ссылка][15]  | [RASPTICKETS-16176][t8]     |
| pobeda3.py                | [Ссылка][16]  | [RASPTICKETS-16657][t9]     |
| pobeda4.py                | [Ссылка][17]  | [RASPTICKETS-17354][t10]    |
| pobeda5.py                | [Ссылка][18]  | [RASPTICKETS-17576][t11]    |
| pobeda6.py                | [Ссылка][19]  | [RASPTICKETS-16501][t12]    |
| pobeda7.py                | [Ссылка][20]  | [RASPTICKETS-16501][t12]    |
| rusline2.py               | [Ссылка][21]  | [RASPTICKETS-7185][t13]     |
| rusline3.py               | [Ссылка][22]  | [RASPTICKETS-10266][t14]    |
| rusline4.py               | [Ссылка][23]  | [RASPTICKETS-18235][t15]    |
| s_seven3.py               | [Ссылка][24]  | [RASPTICKETS-10412][t16]    |
| s_seven4.py               | [Ссылка][25]  | [RASPTICKETS-13920][t17]    |
| s_seven5.py               | [Ссылка][26]  | [RASPTICKETS-14759][t18]    |
| uralairlines.py           | [Ссылка][27]  | [RASPTICKETS-15270][t19]    |
| uralairlines2.py          | [Ссылка][28]  | [RASPTICKETS-19299][t20]    |
| utair.py                  | [Ссылка][29]  | [RASPTICKETDAEMON-374][t21] |
| uzairways2.py             | [Ссылка][30]  |                             |
| uzairways3.py             | [Ссылка][31]  | [RASPTICKETS-10266][t22]    |

[1]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot.py?rev=7439707
[2]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot2.py?rev=7439707
[3]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot2_white_monday.py?rev=7439707
[4]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot3.py?rev=7439707
[5]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot3_plus.py?rev=7439707
[6]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot3_plus_ru.py?rev=7439707
[7]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aeroflot3_ru.py?rev=7439707
[8]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/amargo2.py?rev=7439707
[9]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/aviakass4.py?rev=7439707
[10]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/ctrip.py?rev=7439707
[11]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/ctrip2.py?rev=7439707
[12]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/expressavia3.py?rev=7439707
[13]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/gotogate.py?rev=7439707
[14]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/ozon.py?rev=7439707
[15]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/pobeda2.py?rev=7439707
[16]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/pobeda3.py?rev=7439707
[17]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/pobeda4.py?rev=7439707
[18]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/pobeda5.py?rev=7439707
[19]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/pobeda6.py?rev=7439707
[20]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/pobeda7.py?rev=7439707
[21]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/rusline2.py?rev=7439707
[22]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/rusline3.py?rev=7439707
[23]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/rusline4.py?rev=7439707
[24]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/s_seven3.py?rev=7439707
[25]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/s_seven4.py?rev=7439707
[26]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/s_seven5.py?rev=7439707
[27]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/uralairlines.py?rev=7439707
[28]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/uralairlines2.py?rev=7439707
[29]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/utair.py?rev=7439707
[30]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/uzairways2.py?rev=7439707
[31]: https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/ticket_daemon/ticket_daemon/partners/uzairways3.py?rev=7439707

[t1]: https://st.yandex-team.ru/RASPTICKETS-8841
[t2]: https://st.yandex-team.ru/RASPTICKETS-19097
[t3]: https://st.yandex-team.ru/RASPTICKETS-8706
[t4]: https://st.yandex-team.ru/RASPTICKETS-10011
[t5]: https://st.yandex-team.ru/RASPTICKETS-16467
[t6]: https://st.yandex-team.ru/RASPTICKETS-10266
[t7]: https://st.yandex-team.ru/RASPTICKETS-16303
[t8]: https://st.yandex-team.ru/RASPTICKETS-16176
[t9]: https://st.yandex-team.ru/RASPTICKETS-16657
[t10]: https://st.yandex-team.ru/RASPTICKETS-17354
[t11]: https://st.yandex-team.ru/RASPTICKETS-17576
[t12]: https://st.yandex-team.ru/RASPTICKETS-16501
[t13]: https://st.yandex-team.ru/RASPTICKETS-7185
[t14]: https://st.yandex-team.ru/RASPTICKETS-10266
[t15]: https://st.yandex-team.ru/RASPTICKETS-18235
[t16]: https://st.yandex-team.ru/RASPTICKETS-10412
[t17]: https://st.yandex-team.ru/RASPTICKETS-13920
[t18]: https://st.yandex-team.ru/RASPTICKETS-14759
[t19]: https://st.yandex-team.ru/RASPTICKETS-15270
[t20]: https://st.yandex-team.ru/RASPTICKETS-19299
[t21]: https://st.yandex-team.ru/RASPTICKETDAEMON-374
[t22]: https://st.yandex-team.ru/RASPTICKETS-10266
