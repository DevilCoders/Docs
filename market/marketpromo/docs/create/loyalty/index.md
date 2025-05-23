# Заведение акций через лоялти

Заведение промокодов, кешбека и маркет бонусов через [админку лоялти](https://admin.market-loyalty.market.yandex-team.ru)

[Админка в тестинге](https://admin.market-loyalty.tst.market.yandex-team.ru)

## Как получить доступ
Доступ можно получить через idm

Прод: https://idm.yandex-team.ru/system/market-loyalty
Тестинг: https://idm.test.yandex-team.ru/system/market-loyalty

### Описание ролей
[Описание в коде](https://a.yandex-team.ru/arc_vcs/market/loyalty/market-loyalty-core/src/main/java/ru/yandex/market/loyalty/core/model/security/AdminRole.java)

Скорее всего вам нужна одна из ролей:
1. _Редактирование SmartShopping-акций_ - создание и редактирование новых промокодов и купонов
18. _Редактор кэшбек акций_ - создание и редактирование кешбек акций
2. _Доступ на просмотр_ - просмотр большинства страниц админки лоялти
1. _Редактирование купонных акций_ - создание и редактирование старых/генерируемых промокодов

Описание остальных ролей:
1. _Администратор_ - доступ ко всем функциям админки
3. _Генерация купонов_ - используется для автоматической генерации старых промокодов
4. _Генерация монеток_ - используется маркетингом для генерации монет
5. _Генерация хешей_ - не использовали в течение года
6. _Доступ к небезопасным функциям админки_ - доступ для разработчиков
8. _Инженер по тестированию_ - для сброса кеша перков, других доступов нет
9. _Пользователь с доступом к созданию акций для стрельб_ - для нагрузочного тестирования
10. _Пользователь с доступом к функционалу отбора купонов_ - отбор сорри купонов
11. _Редактирование 3р-акций_ - устаревшая, использовалась для создания старых 3р акций
12. _Редактирование акций начисления_ - создание акции начисления кэшбэка
13. _Редактирование групп акций_ - не использовали в течение года
14. _Редактирование настроек для регионов_ - не использовали в течение года
15. _Редактирование начислений_ - работа с автоматическими начислениями монет, кешбека
16. _Редактирование триггеров_ - устаревшая, использовалась для редактирования триггеров старых промокодных акций
17. _Редактирование флеш-акций_ - устаревшая
19. _Редактор секретных распродаж_ - устаревшая, использовалась для создания старых секретных распродаж

## Доступные акции
1. [Промокод](promo_code.md)
2. [Купон](coin.md)
3. [Кешбек](cashback.md)
