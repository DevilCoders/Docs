## Сервис Яндекс.Аренда

Яндекс.Аренда - сервис для сдачи квартир. Собственник оставляет у нас заявку, мы сами находим жильцов, заселяем их, оформляем страховку, а дальше жильцы делают переводы через личный кабинет.

### Полезные ссылки

- [Прод](https://arenda.yandex.ru)
- [Тестинг](https://arenda.test.vertis.yandex.ru)
- [Админка в тестинге](https://arenda.test.vertis.yandex.ru/management/manager/flats/)
- [Инструкция получения доступа к админке](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-arenda/docs/idm.md)
- [Дашборд с задачами Аренды](https://st.yandex-team.ru/agile/board/5985)
- [Шаблон для заведения задач](https://st.yandex-team.ru/createTicket?template=7872&queue=REALTYBACK)

### Как подключиться к тестовому API

- Открыть по ссылке [тестовый сваггер к REST API](http://realty-rent-api-main.vrts-slb.test.vertis.yandex.net/swagger/)
- Установить [grpcui](https://github.com/fullstorydev/grpcui)
- Подключиться к GRPC API:

  `./grpcui -plaintext realty-rent-api-grpc.vrts-slb.test.vertis.yandex.net:80`

### В помощь дежурному

- [Как делать правки в ДА](https://st.yandex-team.ru/REALTYBACK-6283#615c1a092f31fa50315affd7)
- [Как делать правки в ДСках](https://st.yandex-team.ru/REALTYBACK-6335#61bc7b1a586f576e46883319)
- [Как обновить токены в апи Манго](https://st.yandex-team.ru/REALTYBACK-6825#61c03d0224fba31352bdfd2f)
- [Как удалить персональные данные пользователя](https://st.yandex-team.ru/REALTYBACK-6956#61e81139ce8d641aa08d71b5)
- [Как перепривязать жильца в ДА](https://st.yandex-team.ru/REALTYBACK-7274#621c9887f8e41f0313a9e231)
- [Как заапрувить анкету жильца](https://wiki.yandex-team.ru/realty/backend/realty-rent/tenant-questionnaire-moderation/)
