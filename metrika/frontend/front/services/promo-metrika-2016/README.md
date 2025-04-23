# Метрика промо 2016 [![Build Status](http://drone-beta.haze.yandex.net/api/badges/Metrika/promo-merika-2016/status.svg)](http://drone-beta.haze.yandex.net/Metrika/promo-merika-2016)

Продакшн - https://metrika.yandex.ru/about

## Танкер

https://tanker.yandex-team.ru/?project=promo-metrika-2016
Для импорта ключей нужно использовать команду
Для авторизации в Танкере нужен OAuth токен с доступом к проекту. Подойдёт tanker-token из https://nda.ya.ru/t/8LEJwJwd4wZaJC

    TANKER_API_TOKEN=AAA... npm run i18n

## Бункер

https://bunker.yandex-team.ru/promo-metrika-2016
Ключи импортируются автоматически в зависимомти от окружения выставляется период автообновления ключей
На dev среде период самый мальенький на проде самый больщой

#### Инструкция по работе с Бункером

https://wiki.yandex-team.ru/sales/marketing/advertising/howto/

#### Настройка бункера

https://wiki.yandex-team.ru/verstka/tools/bunker/stuff/

https://bunker.yandex-team.ru/.schema/json-schema-draft-03?view=raw
