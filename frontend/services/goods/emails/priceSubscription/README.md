# Шаблон письма для рассылки уведомлений о измении лучшей цены на товар

Исходная верстка и шаблон письма для рассылки пользователеям, которые подписались в карточки SKU на отслеживание за снижением цены, уведомлений о измении лучшей цены на товар, реализованная в рамках тикета [GOODS-2723: [US] Подписка на изменение цены](https://st.yandex-team.ru/GOODS-2723).

## Список файлов

- `/attachments` - список ресурсов к верстке
- `index.html` - исходная верстка, реализованная в рамках тикета [COMMDESIGN-10292](https://st.yandex-team.ru/COMMDESIGN-10292)
- `index.html.jinja` - [jinja](https://jinja.palletsprojects.com/en/3.1.x/templates/) шаблон письма используемый в рассыляторе

## Периодические рассылки Яндекс Товары

- рассылка в [тестовом рассыляторе](https://test.sender.yandex-team.ru/products/campaign/periodic/)
- рассылка в [продовом рассыляторе](https://sender.yandex-team.ru/products/campaign/periodic/)
