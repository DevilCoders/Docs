## Биллинг логистических партнёров

[Wiki](https://wiki.yandex-team.ru/market/3pl/development/backend/billing/)

Обязанности:
* сбор данных для расчета, сколько денег мы должны заплатить партнёрам (ПВЗ, Курьерские компании, и т.д), и наоборот;
* расчет задолженностей;
* отправка результата в учётные системы (Баланс, OEBS);
* получение информации о платежах партнёров, и помощь в контролировании задолженностей партнёров, а также их отключении.

### Локальный запуск через IDEA

1. Создаем конфигурацию запуска Application.

    - *Main class*:           `ru.yandex.market.tpl.billing.TplBilling`.
    - *Environment vars*:     `PROPERTIES_DIR=<path_to_properties.d>;billing.yt.token=<твой токен>;environment=local;tvm.alias=tpl-billing-test;tvm.client-id=2026914;tvm.secret=<тестовый секрет>
    yt token получается тут - https://yt.yandex-team.ru/docs/description/common/auth#getting_token
    TVM secret смотреть тут - https://abc.yandex-team.ru/services/marketlogistics/resources/?view=consuming&layout=table&supplier=14&show-resource=28880275, нужна роль SSH пользователь в https://abc.yandex-team.ru/services/marketlogistics

    - *Program arguments*:    `local`

1. Запускаем конфигурацию.
