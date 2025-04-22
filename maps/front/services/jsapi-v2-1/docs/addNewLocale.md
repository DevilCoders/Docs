Добавление новой локали:

1. Заказать добавление новой локали в библиотеке localeutils (инфу см. тут https://wiki.yandex-team.ru/maps/dev/core/i18n/localeutils/).
Ответственный uht@. На дев-сервер для тестирования пакет нужно поставить самостоятельно.
2. Заказать добавление локали в танкере для проекта mapsapi и geobases (https://tanker.yandex-team.ru/?project=maps_api&branch=master и https://tanker.yandex-team.ru/?project=geobases&branch=master&keyset=distance)
3. Заказать перевод нужных кейсетов в танкере (geobases переводится полностью, а в mapsapi можно выбрать только нужное заказчику, например для БЯК делаем перевод Traffic, Copyrights, Control.Ruler и route)
4. Заказать добавление локали в regional-units-data (она нужна сервису дорожных событий). Ответственный dieash@.
5. Убедиться, что для локали прописан маппинг в какой-то дефолтный язык.
Список настроенных фолбеков есть тут https://doc.yandex-team.ru/Tanker/general-info/concepts/fallbacks.html
4. Прописать ссылки на ПС в hosts https://github.yandex-team.ru/maps/hosts
5. Прописать локаль в `config/locales.json`
6. Апнуть в Dockerfile версии пакетов yandex-maps-config-hosts и libyandex-maps-localeutils
