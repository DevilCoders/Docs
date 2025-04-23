# FAQ. Расширение компонентов из Лего

__Важно:__ Если не следовать этой инструкции, то вы гарантированно привезете лишний код на клиент.

Расширение делается так (на примере `Icon`):

1. Создаем платформенные папки `src/components/Icon/{desktop,touch-phone,...}`
2. В каждой папке заводим 2 файла: `index.ts` и `package.json`:

    - В `index.ts` реэкспоритуем код компонета из Лего и проектный код:

    ```ts
    export * from '@yandex-lego/components/Icon/desktop';

    // здесь в качестве примера проектного кода набор дополнительных типов Icon
    export * from '../_type';
    ```

    - В `package.json` заводим описание [сайдэффектов](https://webpack.js.org/guides/tree-shaking/#mark-the-file-as-side-effect-free):

    ```json
    {
        "name": "src-icon-desktop",
        "version": "0.0.0",
        "main": "./index.ts",
        "module": "./index.ts",
        "sideEffects": [ <-- самое важное место
            "*.css",
            "*.scss"
        ]
    }
    ```

Теперь при использовании Icon из проекта webpack поймет, какой код можно безболезненно отрезать при сборке чанков, как неиспользуемый в рамках чанка.

### Как не нужно организовывать код

Если в `src/components/Icon/index.ts` напишем

```ts
// реэкспортируем компонент из Лего
export * from '@yandex-lego/components/Icon';

// дальше экспортируем всё, что добавили в проекте
export { IWithTypeCalendarProps } from './_type/Icon_type_calendar';
/* остальные проектные доопределения... */
```

то webpack не поймет, что внутри `@yandex-lego/components/Icon` есть какой-то лишний код.

### Особенности сборки кнопки
Если вас по каким-то причинам не устраивает собранная кнопка из `@components/Button`, то вы можете собрать ее сами.

```ts
import {
    Button as ButtonBase,
    withSizeM,
    withViewAction,
} from '@yandex-lego/components/Button/touch-phone'

const Button = compose(
    withSizeM,
    withViewAction,
)(ButtonBase)
```

Нам также потребуются счетчики для нашей кнопки и их настройка несколько нетривиальна. Нужно импортировать HOC
`withTypeLink` из `@components/Button` и применять в compose после `withBaobab`.

```ts
import { withBaobab } from '@yandex-int/react-baobab-logger';
import { withTypeLink } from '@components/Button/Button@touch-phone';

const Button = compose(
    withBaobab({ name: 'button' }),
    withTypeLink,
    withSizeM,
    withViewAction,
)(ButtonBase)
```

### Когда станет лучше

Есть набор issue

- [9607](https://github.com/webpack/webpack/issues/9607)
- [9078](https://github.com/webpack/webpack/issues/9078)
- [8951](https://github.com/webpack/webpack/issues/8951)

описывающих схожую проблему.

Исправлять в web4 будем в рамках задачи [SERP-92106](https://st.yandex-team.ru/SERP-92106)
