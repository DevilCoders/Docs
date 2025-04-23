## Как добавить контрол в схему
Панель для изменения значений слоя строится из двух моделей.

Модель схем `client/models/scheme-model.ts`. Главная особенность модели - не содержит данные,
только то для чего требуется отображение контрола.

Store для слоев создается на основании захардкоженых в проекте схем в `client/schemes/`
для каждого типа слоя.

Каждая схема содержит названия табиков, названия групп и label самого контрола.

Каждый контрол описывается объектом:
```typescript
{
    // Название поля стиля https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/renderer/style/0.x/schema/types/style-fill-extrusion.json?rev=3807538
    setting: 'text-field',

    // тип в модели mobx-state-tree https://github.com/mobxjs/mobx-state-tree#types-overview
    type: optional(string, ''),

    // лейбочка для отображения.
    label: 'Field',

    // контрол из client/common/core/available-controls/available-controls.ts
    control: 'SelectControl',

    // Дополнительные props прокдываемые в контрол.
    props: {
        items: []
    }
}
```

По полю `setting` во вью мы получаем данные для этого поля из бекенда.
Пример ответа бекенда есть в `server/api-stub/get-layers.api.js`.

#### Замечание.
`control` это только название контрола, а не его класс. Если добавляете новый
контрол, то его также нужно добавить в хеш `CONTROLS` в `client/common/core/available-controls/available-controls.ts`

`type` - тип поля в модели MobX.

При добавлении контрола не забудьте добавить его схему валидации.
То, как проверить данные от контрола
`client/validation-schemas/backend/validator.ts` `mapControlNamesToScheme()`
Ну и вам typescript если забудете добавить схему :).
