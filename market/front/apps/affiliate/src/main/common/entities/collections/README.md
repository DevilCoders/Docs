# Базовые типы и хелперы для работы с коллекциями

## Опциональность при работе с коллекциями

При написании типа для объекта с коллекциями мы используем опциональные поля.

### 1. Наличие конкретных ключей в объекте с коллекциями зависит от параметров запроса к бэкенду

Бэкенды - это основной источник данных для создания коллекций,
потому опционалньость исходит из того, что мы должны уметь получать сущности частями. 

Например коллекции могут быть описаны как `Collections<Category | Model>`,
но при этом, в ряде случаев, мы не будем передавать в запрос к бэкенду поле `'MODEL_CATEGORY'`,
что приведет к тому, что при нормализации поле `'category'` в объекте коллекций
создано не будет.

Тип `Collections<Model | Offer | Sku>` следует читать так,
что в объекте с коллекциями могут быть коллекции с сущностями `Model`, `Offer`, или `Sku`,
но не обязательно, что они там есть.

### 2. Опциональность поощряет работу через геттеры

Использование специальных хелперов предпочтительнее,
чтобы в случае ошибок получать `AssertionError` вместо `TypeError`.
Также использование хелперов уменьшает написание шаблонного кода.

```ts
const collections: Collections<Model> = {};
const model1: Model = collections?.model?.[123];
//    ^^^^^^
//    Type 'Model | undefined' is not assignable to type 'Model'.

const model2: Model = getCollectionsModelById(123, collections);
// или
const model3: Model = getCollectionsSpecificEntityById(EntityTypes.Model, 123, collections);
//                    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
//                    Получаем AssertionError, если такой сущности нет в объекте с коллекциями.
```

### 3. Безопасное получение сущности из объекта с коллекциями

В ряде случаев, перед полученим сущности по ее `id`,
нам необходимо проверить, что такой `id` есть в объекте с коллекциями, 
и только после этого уже пытаться применять геттер.

Для таких ситуаций используйте специальные `find` хелперы вместо оператора "точка".

**Плохой вариант**

```ts
const collections: Collections<Model> = {};
const modelId: ModelId = 123;
const model: Model | undefined = collections?.model?.[modelId];

if (model) {
    ...
}
```

**Хороший вариант**

```ts
const collections: Collections<Model> = {};
const modelId: ModelId = 123;
const model: Model | undefined = findCollectionsModelById(modelId, collections);

if (model) {
    ...
}
```