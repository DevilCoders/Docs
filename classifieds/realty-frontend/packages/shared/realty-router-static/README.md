# realty-router-static

Инстанс `realty-router` с синхронными урлами (не использующими json-маппинги из `realty-router/data/`).
---
\
Нужен для постепенного отказа от использования `realty-router` на клиенте.
Будем переключать построение ссылок на него, а за урлами, в которых используются json'ы из `realty-router/data/` будем ходить в `realty-router-api`.
