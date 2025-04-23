# Merge Queue Spotlight

**Merge Queue Spotlight (MQS)** — пользовательский интерфейс (UI), отображающий состояние очереди.
Расположен по адресу [mqs.si.yandex-team.ru][mqs].

![Пример отображения очерёдности](../assets/mqs.png)

Непосредственно на процесс влития MQS не влияет и предоставляется для отображения очерёдности, а также общего состояния механизма: остановлен или работает штатно.

[mqs]: https://mqs.si.yandex-team.ru

## <a name="access"></a> Доступ

На данный момент из-за [отсутствия аутентификации][mq-auth] интерфейс доступен только при наличии сетевого доступа (дырки в файрволе).

Заказать можно через [форму в Puncher][puncher]:

- Назначение, протокол (TCP) и порты (`80`, `443`) в форме предзаполнены.
- Источником нужно указать сервисную роль (скоуп) в ABC, привязанном к вашему проекту. Например: [Разработка (Фемида)][femida-dev].
- ⚠️ Доступ не выдаётся по логинам или Стафф-группам.

[mq-auth]: https://st.yandex-team.ru/FEI-21328
[puncher]: https://puncher.yandex-team.ru?create_destinations=mqs.si.yandex-team.ru&create_protocol=tcp&create_locations=office,vpn&create_ports=80,443
[femida-dev]: https://abc.yandex-team.ru/services/825?scope=development
