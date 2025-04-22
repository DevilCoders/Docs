# Микроформат BVL

Блок содержит в себе информацию о лицензиаре, франшизе или персонаже.

## Параметры
- **id** `<number>` – уникальный идентификатор – обязательный параметр
- **type** `<enum>` – тип – обязательный параметр
    - `licensor` – лицензиар
    - `franchise` – франшиза
    - `character` – персонаж
- name `<string>` – название
- logo [`<picture>`](https://github.yandex-team.ru/market/microformats/tree/master/picture) – изображение логотипа
- bindings `<bvl[]>` – связи с другими сущностями BVL
