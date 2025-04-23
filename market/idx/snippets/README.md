# Сниппеты в поиске Яндекса
Не путать с подготовкой сниппетов при сборке полных маркетных поколений!

## Документация
Техническая:
- https://wiki.yandex-team.ru/market/development/indexer/snippet

Продуктовая:
- https://yandex.ru/support/partnermarket/efficiency/snippets.html#add
- https://wiki.yandex-team.ru/market/support/marketb2b/publicat/snippets/
- https://wiki.yandex-team.ru/market/projects/market4serp/snippets/

## Сборка
Building package:
```
$ [YT_TOKEN_PATH=$HOME/.yt/token] YT_USER=$USER debuild -eFEEDPARSER_PATH -e{YT_TOKEN,YT_TOKEN_PATH} -eYT_PROXY -eYT_USER
```
Pass YT_TOKEN if that's how you define it, or else pass the YT_TOKEN_PATH (make sure it's absolute).
