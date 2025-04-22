# Работа с экспериментами

Все пути и операции описаны относительно директории нужного проекта.

Первый шаг - добавить флаг в `src/experiments/flags.ts` и обязательно заполнить все поля.

**Название флага влияет на то, подключится ли эксперимент на страницу или нет.
Важно четко указывать место использования в названии, чтобы с одной стороны - не потерять функционал, с другой - не загрузить лишний бандл на страницу**
1. Определите на каком сервисе, платформе, странице будет использоваться флаг (подключаться эксперимент)
2. Исходя из места его испольования, назовите флаг в соответствии с форматом `yxneo_${EService}_${EPlatform}_${EPage}_feature-name`, где:
- `EService` - сервис из `neo/types/EService`
- `EPlatform` - платформа (touch|desktop) из `neo/types/EPlatform`
- `EPage` - страница сервиса из `<service>/types/EService`
- `TPage` - любая страница из `neo/expreriments/flags` (иногда нужно, чтобы флаг приходил не на все, но на любую указанную в эксперименте страницу)
Если флаг должен приходить на все `сервисы|платформы|страницы`, то соответсвующий enum в названии флага можно пропустить.
3. Перечисления в названии флага поддерживают union `EPage.MAIN | EPage.STORY` и exclude `Exclude<EPage, EPage.RUBRIC>`
4. **Примеры**
- `yxneo_feature-name` - флаг для всех страниц
- `yxneo_${EService.SPORT}_feature-name` - эксперимент для всех страниц на тачах или десктопе cпорта
- `yxneo_${EService.SPORT}_${EPlatform.TOUCH}_${EPage.MAIN | EPage.RUBRIC}_feature-name` - эксперимент для тачевой главной и рубрики спорта
- `yxneo_${EService.SPORT}_${Exclude<EPage, EPage.EVENT>}_feature-name` - эксперимент для всех страниц спорта, кроме страницы события
- `yxneo_${EService.SPORT}_${EPlatform.DESKTOP}_${EPage.STORY}_feature-name` - эксперимент для десктопного сюжета спорта

### Получить значение флага

На клиенте нужно использовать `src/hooks/useFlag`, на сервере `src/helpers/getFlag`.
Оба хелпера принимают тип, к которому следует привести значение флага. Тип должен совпадать с указанным во `flags.ts` - это проверяется тайпскриптом.

### Бандл для эксперимента

1. Тип флага должен быть `boolean` или `number` (для обратной совместимости с прошлой реализацией).
1. Создать директорию с названием флага в `src/experiments/`
1. Создать в ней файл `index.ts`, который экспортирует дефолтно (это важно!) экспериментальный код (компоненты, функции, объекты, строки, ...)

**Пример:**
```ts
// <serviceOrPackage>/src/experiments/yxneo_my-flag/index.ts
import { ExpComponent } from './ExpComponent';
import { AnotherExpComponent } from './AnotherExpComponent';

const expNewValue = 100;

export default {
  component: ExpComponent,
  anotherComponent: AnotherExpComponent,
  newValue: expNewValue,
};
```

#### Использование бандла

Для рендера компонентов из бандла эксперимента нужно использовать компонент `src/components/Exp/Exp`.

**Сигнатура:** `<Exp flag=<string> get=<string> props?={object}>{children?}</Exp>`
* `flag` — Название флага.
* `get` — Название свойства, которое необходимо взять из экспорта вышеуказанного `index.ts`.
* `props?` — Пропсы, которые будут переданы экспериментальному компоненту.
* `children?` — Передаётся то, что будет выведено с выключенным флагом.

**Пример**

```tsx
import { Exp } from '<serviceOrPackage>/components/Exp/Exp';

// В эксперименте отрендерится компонент из бандла `yxneo_my-flag` (из свойства `component`)
// Если флаг выключен, то отрендерится компонент `ComponentWithoutFlag`
<Exp flag="yxneo_my-flag" get="component" props={props}>
  <ComponentWithoutFlag {...props} />
</Exp>
```

Для получения других значений из бандлов - `src/hooks/useExp`:

**Сигнатура:** `useExp<T>(flag: string, get: string, fallback?: T): T`
* `flag` — Название флага.
* `get` — Название свойства, которое необходимо взять из экспорта вышеуказанного `index.ts`.
* `fallback?` — В случае если флаг выключен, `useExp` вернёт этот параметр.

```ts
// <serviceOrPackage>/src/experiments/yxneo_my-flag/index.ts
export default {
  foo: '__bar__',
  component: BazComponent
};

// someComponent.tsx
import { useExp } from '<serviceOrPackage>/hooks/useExp';

// получить значение свойства 'foo' из бандла если флаг включен,
// иначе получить '__fallback__'
const foo = useExp('yxneo_my-flag', 'foo', '__fallback__');

```

### Переопределение экспериментов

Эксперименты могут быть получены из следующих источников:

* `@yandex-sport/core/src/experiments` - общие эксперименты
* `@yandex-sport/mg/src/experiments` - эксперименты, относящиеся к общим компонентам. Здесь можно переопределить эксперименты из `@yandex-sport/core`
* `<serviceOrPackage>/src/experiments` - эксперименты компонент, разрабатываемых в service или package. Здесь можно переопределить эксперименты из `@yandex-sport/core`, `@yandex-sport/mg`

Для переопределения нужно добавить папку с именем переопределяемого эксперимента. Например, можно изменить стили

```ts
// <serviceOrPackage>/src/experiments/yxneo_my-flag/index.ts
import exp from 'mg/experiments/yxneo_my-flag';
import './style.scss';

export default exp;
```

### Типичные проблемы:

1. Проблема - нерабочий флаг на странице. Эксперимент (бандл, флаг) не приходит на клиент, т.к. флаг описан для другой страницы, сервиса и т.д. Например, флаг(бандл) yxneo_news_{EPage.STORY}_feat будет приходить только для новостей, на страницу сюжета.

2. Лишний флаг на странице. Флаг приходит на клиент для тех страниц, для которых не должен (может в том числе пересечься с другим экспериментом и поломать стили одного веса).
   Например, флаг `yxneo_${EService}_feature` придет на все страницы определенного сервиса, если его раскатят в эксперимент.
   Флаг `yxneo_sport_desktop_main_feature` - невалидное именование (должно быть `yxneo_${EService.SPORT}_${EPlatform.Desktop}_${EPage.MAIN}_feature`) - так же придёт на всё страницы.
