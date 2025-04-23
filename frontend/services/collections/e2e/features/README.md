# Документация:
* [дока fiji](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/docs/yaml.md)

## Список тегов
https://wiki.yandex-team.ru/users/next0/collections-bug-tags/

## Структура

_Названия пишутся через дефис, начинаются с глаголов, затем добавляются дополнительные параметры(при необходимости)_

    features/[platform]/[feature-entity]/[verb]-[entity]-[some-modifiers]/[verb]-[entity]-[some-modifiers].e2e.ts
    features/[platform]/[feature-entity]/[verb]-[entity]-[some-modifiers]/[verb]-[entity]-[some-modifiers].yml

    эксперименты кладутся в папку _experiments остальные правила сохраняются
    features/[platform]/[feature-entity]/_experiments/[verb]-[entity]-[some-modifiers]/[verb]-[entity]-[some-modifiers].e2e.ts
    features/[platform]/[feature-entity]/_experiments/[verb]-[entity]-[some-modifiers]/[verb]-[entity]-[some-modifiers].yml

**Примеры:**

1. Десктопный тест на лайк карточки неавторизованным пользователем.
    ```
    features/desktop/cards/like-card-unauth/like-card-unauth.e2e.ts
    features/desktop/cards/like-card-unauth/like-card-unauth.yml
    ```
2. Десктопный тест подписки на борду из рекомендаций к борде
    ```
    features/desktop/boards/subscribe-board-recomendations/subscribe-board-recomendations.e2e.ts
    features/desktop/boards/subscribe-board-recomendations/subscribe-board-recomendations.yml
    ```
3. Десктопный тест на добавление карточки с типом "Изображение"
    ```
    features/desktop/add-flow/add-card-image/add-card-image.e2e.ts
    features/desktop/add-flow/add-card-image/add-card-image.yml
    ```
4. Десктопный тест на эксперимент с добалением карточки с типом "Изображение"
    ```
    features/desktop/add-flow/_experiments/add-card-image/add-card-image.e2e.ts
    features/desktop/add-flow/_experiments/add-card-image/add-card-image.yml
    ```
5. Десктопный тест на редактирование карточки с типом "Изображение"
    ```
    features/desktop/add-flow/edit-card-link/edit-card-link.e2e.ts
    features/desktop/add-flow/edit-card-link/edit-card-link.yml
    ```
6. Десктопный тест на репин карточки (для всех типров карточки одиноково)
    ```
    features/desktop/add-flow/repin-card/repin-card.e2e.ts
    features/desktop/add-flow/repin-card/repin-card.yml
    ```

```
├── features
│   ├── desktop
│   │   ├── add-flow
│   │   │   ├── _experiments - тесты на эксперименты
│   │   │   │   ├── add-card-image
│   │   │   │       ├── add-card-image.e2e.ts
│   │   │   │       ├── add-card-image.yml
│   │   │   │
│   │   │   ├── add-card-image
│   │   │       ├── add-card-image.e2e.ts
│   │   │       ├── add-card-image.yml
│   │   │
│   │   ├── profile
│   │   │   ├── ...
│   │   │
│   │   ├── boards
│   │   │   ├── subscribe-board-recomendations
│   │   │       ├── ...
│   │   │
│   │   ├── cards
│   │   │   ├── open-card-link
│   │   │       ├── ...
│   │   ├── ...
│   │
│   ├── mobile
│   ├── ...
```

## Не забыть:
* Проставлять тег backend, для тестов, где у фичи есть бэкенд
* Проставлять поле tlds:
  - all - если фича работает на всех поддерживаемых доменах
  - [ru, by] - если фича работает на доменах ru, by
* Не использовать в тестах ссылки на внешние ресурсы

## Полезное:
* [про lable](https://clubs.at.yandex-team.ru/search-interfaces/26170)
* [о чём не забыть когда пишешь ямлы](https://wiki.yandex-team.ru/serp/tolokaserp/#ochjomnezabytpodumatkogdapisheshjamly)
