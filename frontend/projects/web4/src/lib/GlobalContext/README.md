# Глобальный контекст запроса

**GlobalContext** — объект, являющийся главным хранилищем данных по запросу.

Обладает свойствами:

1. Читает данные напрямую из данных бекенда (`reqdata`, `apphost`, etc) так:
  * Читает/обрабатывает данные лениво, только при явном обращении
  * Прочитанные данные фризит и кеширует
2. Все прочие контексты в проекте расширяют GlobalContext

## FAQ

### Как прочитать данные из GlobalContext?

Если под рукой есть любой контекст (в priv-ах - конструкторский контекст, в ts - это `this.context`), читаем из него (см, свойство 2).

Если под рукой нет контекста, читаем из `RequestCtx.GlobalContext`.

### Как добавить новое поле в GlobalContext?

1. Дописать код, достающий данные для нового поля в [props](./props).
2. Добавить новое поле в [props/index](./props/index.js) (или `index@{platform}.js` если изменение касается конкретной платформы)
3. Добавить [typescript-код](./index.d.ts) и [jsdoc](../../../construct/blocks-common/construct/__context/construct__context.priv.js) для нового поля

> Существует альтернативный и удобный способ добавления нового поля в GlobalContext - воспользоваться кодогенерацией, вызвать ее можно по команде `npm run generate:global-context-field`, подробнее о возможностях кодогенератора можно прочитать в [документации](../../../docs/generators/README.md)

### Может ли поле в GlobalContext зависеть от флагов? А зависеть от другого поля в GlobalContext?

Да, смотрите на уже реализованные поля.

### Можно ли добавить изменяемое поле в GlobalContext?

Если нужно добавить в GlobalContext поле, в которое предполагается писать, вы неминуемо упретесь в "фризинг" (см. в свойства 1).

Изменяемые поля должны жить в другом месте. Пока таким местом являются наследники GlobalContext-а (см. где живут поля `answerTheme` и прочие).

## Примеры использования полей
- [bigB](../../../src/features/LearnSerpBigB/README.md)
