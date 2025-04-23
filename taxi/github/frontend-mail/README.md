Яндекс.Такси - верстка писем
============================

Сборка письма - инлайн стилей

```bash
grunt build:199
```

Отправка письма

```bash
grunt sendMail:249 --to=frgt@yandex-team.ru
grunt sendMail:check --to=frgt@yandex-team.ru --upload=false
```

### Письма

- 199 - [TXI-1025](https://st.yandex-team.ru/TXI-1025)
- 249 - [TXI-1123](https://st.yandex-team.ru/TXI-1123)
- report - [TXI-1210](https://st.yandex-team.ru/TXI-1210) 1ый макет
- report2 - [TXI-1210](https://st.yandex-team.ru/TXI-1210) 2ой макет
- report2-en - [TXI-1210](https://st.yandex-team.ru/TXI-1210) 2ой макет - en вариант
- 199-spb - [TXI-1250](https://st.yandex-team.ru/TXI-1250)
- confirm - [TXI-1358](https://st.yandex-team.ru/TXI-1358)
- report-uber - [TXI-4570](https://st.yandex-team.ru/TXI-4570)

### Загрузка картинок для отправки писем

TODO ...

```bash
grunt oauth
```

### TODO

[ ] - обновить grunt-email-builder до ~3.0


### Инфо

Превью письма - http://habrahabr.ru/company/pechkin/blog/260945/

https://github.yandex-team.ru/taxi/tools/blob/master/db/ride_report/templates/testing/ride_report/html_body/ru.xhtml
