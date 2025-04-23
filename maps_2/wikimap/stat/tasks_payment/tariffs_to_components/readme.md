Tariffs to Components
=====================
Creates components in [Tracker] queues according to [tariffs].

Usage:

    ./tariffs_to_components [--env <environment>] --tracker-token <token>

Where:
* `<environment>` - Tracker environment: `testing` (default) or `production`;
* `<token>` - Tracker authorization token (can be obtained [here][token]).


[Tracker]: https://st.yandex-team.ru
[tariffs]: /arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/dictionaries/tariff
[token]: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b
