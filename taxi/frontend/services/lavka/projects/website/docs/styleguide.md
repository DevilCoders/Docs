# Styleguide

## Код

- Не используйте дефолтных экспортов

```ts
// Плохо
export default doSomething

// Хорошо
export function doSomething() { ... }
```

- Не используйте классы для создания React-компонентов

```tsx
// Плохо
class MyComponent extends React.Component {
  state = {
    count: 0,
  }

  render() {
    const { count } = this.state

    return <button onClick={() => this.setState({ count: count + 1 })}>Clicked {count} times</button>
  }
}

// Хорошо
import { FC } from 'react'

interface MyComponentProps {
  myProps: string;
}

const MyComponent: FC<MyComponentProps> = () => {
  const [count, setCount] = useState(0)

  return <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>
}
```

- Функции, создаваемые внутри других функций, должны использовать function expressions, в остальных случаях используйте function declaration. 

```tsx
// Плохо
export const foo = () => {
  return "bar";
}

export function CustomButton() {
  function handleClick() {
    console.log('Hello, world!')
  }
  return <button onClick={handleClick}>Print</button>
}

// Хорошо
export function foo(): string {
  return "bar";
}

export function CustomButton() {
  const handleClick = () => {
    console.log('Hello, world!')
  }
  return <button onClick={handleClick}>Print</button>
}
```

- Если функция возвращает `void`, то пишите `return`. Если функция возвращает не `void`, то пишите `return undefined`.

```ts
// Плохо
function getImage(url: string | undefined): string | undefined {
  if (url === undefined) {
    return 
  }
  ...
}

function calculate(a: number, b: number): void {
  if (a === b) {
    return undefined
  }
  ...
}

// Хорошо
function getImage(url: string | undefined): string | undefined {
  if (url === undefined) {
    return undefined
  }
  ...
}

function calculate(a: number, b: number): void {
  if (a === b) {
    return
  }
  ...
}
```

- Используйте тройное равно вместо двойного. Для использования двойного равно должна быть причина.
- Не используйте lodash на клиенте, если нужна небольшая и несложная функция. Для использования lodash должна быть причина (мы заботимся о размере бандла). 
- Разделяйте код на смысловые части с помощью пустых строк.
- В TODO помимо пояснения необходимо указывать ссылку/id задачи на исправление.
- Если обновляете ручку, то повышайте версию ручки на единицу. Новые ручки начинайте с первой версии. Старые ручки удаляйте минимум через месяц: создавайте задачу в бэклоге, ставьте напоминание.
- Логические выражения раскрывайте по закону [де Моргана](https://ru.wikipedia.org/wiki/Законы_де_Моргана): `!( A && B ) = !A || !B`. Но можете не раскрывать, если считаете, что так понятнее.
- Тесты для файла `filename.ts` должны лежать рядом с именем `filename.test.ts`
- Предпочитайте функции, а не классы
- Указывайте тип возвращаемого значения функции, если хотите его зафиксировать или считаете это необходимым.
- Используйте оптимистичные апдейты в памяти стейта там где это возможно
- Используйте интерфейсы вместо типов. Для использования типов должна быть причина. 
- Имена типов и интерфейсов следует писать в `PascalCase`, префиксы в типах не используем

```ts
// Плохо
interface entity { 
  id: string 
}

// Плохо
interface IEntity {
  id: string
}

// Хорошо
interface Entity { 
   id: string 
}
```

- Избегайте использования исключений - если это возможно используйте систему типов для обработки ошибок
- Не используйте пост- или пре- символов подчеркивания

```ts
// Плохо
foo._bar = 'value'
foo.bar_ = 'value'

// Хорошо
foo.bar = 'value'
```

- Возвращайте результат выполнения хуков напрямую.

```ts
// Плохо
function Foo() {
  const myService = useMyService()
  const newService = useMemo(() => myService.createService(), [myService])

  return newService
}

function useMyState() {
  const myState = useContext(MyStateContext)

  return myState
}

// Хорошо
function Foo() {
  const myService = useMyService()
  return useMemo(() => myService.createService(), [myService])
}

function useMyState() {
  return useContext(MyStateContext)
}
```

- Используйте `undefined` вместо `null`. Для использования `null` должна быть причина. 

```ts
// Плохо
function Foo() {
  const ref = useRef(null)

  return //...
}

function getSomething(): Something | null {
  try {
    return doSomething()
  } catch (e) {
    return null
  }
}

// Хорошо
function Foo() {
  const ref = useRef()

  return //...
}

function getSomething(): Something | void {
  try {
    return doSomething()
  } catch (e) {
    return undefined
  }
}
```

- Объявляйте массивы через `[]` для простых типов и через `Array<T>` для сложных.

```ts
// Плохо
const names: Array<string> = ['Misha', 'Sasha']
const values: (string | number)[] = ['one', 1, 'two', 2]

// Хорошо
const names: string[] = ['Misha', 'Sasha']
const values: Array<string | number> = ['one', 1, 'two', 2]
```

- Тело условных операторов и циклов заключайте в фигурные скобки. Кроме проверки условий для досрочного выхода из функции. 

```ts
// Плохо
if (...) return undefined

for (let i = 0; i < 5; i++) s += i

function run(a: number) {
  if (a === 0) {
    return
  }
  ...
}

// Хорошо
if (...) {
  return undefined
}

for (let i = 0; i < 5; i++) {
  s += i
}

function run(a: number) {
  if (a === 0) return
  ...
}
```

## Стили и линария

Договорились придерживаться одного стиля с `uikit`, подробнее можно прочитать в [STYLEGUIDE.md](../../../packages/ui/STYLEGUIDE.md), тезисно:

- Используем `css()`, не используем `styled()`.
- Для стилей заводим отдельный `*.css.ts` файл рядом с компонентом.
- Все классы из файла сразу экспортируем, импортим через звездочку в переменную `c`.
- В качестве рутового класса используем имя компонента в `PascalCase`, остальные классы пишем в `camelCase` без постфиксов вроде `*ClassName`

Пример:

```tsx
// Component.css.ts
import {css} from 'linaria'

export const Component = css`
  ...
`

export const image = css`
  ...
`

// Component.tsx
import * as c from './Component.css'

// ---

<div className={c.Component}>
  <img className={c.image} src="" alt="">
</div>
```

## Именование переменных

- [Английский язык](#английский-язык)
- [Соглашение](#соглашение)
- [S-I-D](#s-i-d)
- [Избегайте сокращений](#избегайте-сокращений)
- [Избегайте дублирования контекста](#избегайте-дублирования-контекста)
- [Отражайте ожидаемый результат](#отражайте-ожидаемый-результат)
- [Именование функций](#именование-функций)
  - [Шаблон A/HC/LC](#шаблон-ahclc)
  - [Action](#action)
  - [Context](#context)
  - [Prefixes](#prefixes)
- [Единственное и множественное число](#единственное-и-множественное-число)

---

## Английский язык

Используйте английский язык для именования.

```ts
/* Плохо */
const primerNombre = 'Gustavo'
const amigos = ['Kate', 'John']

/* Хорошо */
const firstName = 'Gustavo'
const friends = ['Kate', 'John']
```

## Соглашение

Используйте **только** camelCase для именования переменных

```ts
/* Плохо */
const page_count = 5
const shouldUpdate = true

/* Хорошо */
const pageCount = 5
const shouldUpdate = true
```

## S-I-D

Имя должно быть _коротким (short)_, _интуитивным (intuitive)_ и _описательным (descriptive)_:

- **Short**. Имя должно быть быстро написать и при этом запомнить;
- **Intuitive**. Имя должно читаться натурально, как можно ближе к обычному языку;
- **Descriptive**. Имя должно отражать действие и предназначение.

```ts
/* Плохо */
const a = 5 // "a" может значить что угодно
const isPaginatable = a > 10 // "Paginatable" звучит ненатурально
const shouldPaginatize = a > 10 // Выдуманный глагол

/* Хорошо */
const postCount = 5
const hasPagination = postCount > 10
const shouldPaginate = postCount > 10
```

## Избегайте сокращений

**Не** используйте сокращения. Они не приносят никакой пользы, а только ухудшают читаемость.

```ts
/* Плохо */
const onItmClk = () => {}

/* Хорошо */
const onItemClick = () => {}
```

## Избегайте дублирования контекста

Имя не должно дублировать контекст в котором оно определено (не относится к экспортированным функциям/переменным). Всегда удаляйте контекст из имени, если это не ухудшает читаемость.

```ts
class MenuItem {
  /* Имя метода дублирует контекст ("MenuItem") */
  handleMenuItemClick = (event) => { ... }

  /* Читается нормально `MenuItem.handleClick()` */
  handleClick = (event) => { ... }
}
```

## Отражайте ожидаемый результат

```tsx
/* Плохо */
const isEnabled = itemCount > 3
return <Button disabled={!isEnabled} />

/* Хорошо */
const isDisabled = itemCount <= 3
return <Button disabled={isDisabled} />
```

---

# Именование функций

## Шаблон A/HC/LC

Шаблон именования:

```
prefix? + action (A) + high context (HC) + low context? (LC)
```

Примеры использования паттерна:

| Name                   | Prefix   | Action (A) | High context (HC) | Low context (LC) |
| ---------------------- | -------- | ---------- | ----------------- | ---------------- |
| `getUser`              |          | `get`      | `User`            |                  |
| `getUserMessages`      |          | `get`      | `User`            | `Messages`       |
| `handleClickOutside`   |          | `handle`   | `Click`           | `Outside`        |
| `shouldDisplayMessage` | `should` | `Display`  | `Message`         |                  |

> **Примечание:** Порядок контекста влияет на смысл переменной. К примеру, `shouldUpdateComponent` означает что _вы_ обновляете компонент, при этом `shouldComponentUpdate` говорит что _компонент_ будет обновлен, а вы всего лишь контролируете когда.
> Другими словами, **верхний контекст представляет собой смысл переменной**.

---

## Action

Глагольная часть имени функции. Описывает, что _делает_ функция.

### `get`

Получает данные немедленно (геттер).

```ts
function getFruitCount() {
  return this.fruits.length
}
```

> См. также [create](#create).

### `set`

Устанавливает значение переменной.

```ts
let fruits = 0

function setFruits(nextFruits) {
  fruits = nextFruits
}

setFruits(5)
console.log(fruits) // 5
```

### `reset`

Сбрасывает значение переменной к исходному.

```ts
const initialFruits = 5
let fruits = initialFruits
setFruits(10)
console.log(fruits) // 10

function resetFruits() {
  fruits = initialFruits
}

resetFruits()
console.log(fruits) // 5
```

### `fetch`

Запрашивает данные, что может занять время (асинхронный запрос).

```ts
function fetchPosts(postCount) {
  return fetch('https://api.dev/posts', {...})
}
```

### `remove`

Удаляет что-то _из_ чего-то.

```ts
function removeFilter(filterName, filters) {
  return filters.filter((name) => name !== filterName)
}

const selectedFilters = ['price', 'availability', 'size']
removeFilter('price', selectedFilters)
```

> См. также [delete](#delete).

### `delete`

Удаляет что-то безвозвратно.

```ts
function deletePost(id) {
  return database.find({ id }).delete()
}
```

> См. также [remove](#remove).

### `create`

Создает новые данные из существующих. Можно согласиться на других вариантах (make или compose).

```ts
function createPageUrl(pageName, pageId) {
  return pageName.toLowerCase() + '-' + pageId
}
```

> См. также [get](#get).

### `handle`

Обрабатывает действие. Чаще всего коллбэк.

```ts
function handleLinkClick() {
  console.log('Clicked a link!')
}

link.addEventListener('click', handleLinkClick)
```

---

## Context

Область с которой оперирует функция.

Функция это чаще всего действие над _чем-либо_. Очень важно указать над чем производится действие или ожидаемый результат.

```ts
/* Функция оперирующая над примитивами */
function filter(list, predicate) {
  return list.filter(predicate)
}

/* Функция оперирующая только с постами */
function getRecentPosts(posts) {
  return filter(posts, (post) => post.date === Date.now())
}
```

--

## Prefixes

Префиксы уточняют имя переменной. Они нечасто используются в названиях функций.

### `is`

Описывает характеристику или состояние текущего контекста (обычно `boolean`).

```ts
const color = 'blue'
const isBlue = color === 'blue' // характеристика
const isPresent = true // состояние

if (isBlue && isPresent) {
  console.log('Blue is present!')
}
```

### `has`

Описывает существование значение в текущем контексте (обычно `boolean`).

```ts
/* Плохо */
const isProductsExist = productsCount > 0
const areProductsPresent = productsCount > 0

/* Хорошо */
const hasProducts = productsCount > 0
```

### `should`

Отражает возможность выполнения действия при определенном условии (обычно `boolean`).

```ts
function shouldUpdateUrl(url, expectedUrl) {
  return url !== expectedUrl
}
```

### `min`/`max`

Описывает минимальное или максимальное значение.

```ts
function renderPosts(posts, minPosts, maxPosts) {
  return posts.slice(0, randomBetween(minPosts, maxPosts))
}
```

### `prev`/`next`

Описывает предыдущее либо будущее значение состояния в текущем контексте.

```tsx
function fetchPosts() {
  const prevPosts = this.state.posts

  const fetchedPosts = fetch('...')
  const nextPosts = concat(prevPosts, fetchedPosts)

  this.setState({ posts: nextPosts })
}
```

## Единственное и множественное число

Как и префикс, имя переменной может отражать содержит он одно или множество значений.

```ts
/* Плохо */
const friends = 'Bob'
const friend = ['Bob', 'Tony', 'Tanya']

/* Хорошо */
const friend = 'Bob'
const friends = ['Bob', 'Tony', 'Tanya']
```

## File structure

- В основном при создании новых файлов/пакетов обращайте внимание на существующую структуру и стиль
- Используйте PascalCase для имен файлов, если это React-компонент или файл компаньон (например, `Button.css.ts`). В остальных случаях используйте kebab-case
- Используйте плоскую структуру проекта пока это возможно. Используйте директории для группировки файлов, если уже скопилось много файлов (более 30, исключая тестовые файлы)
- Не создавайте много мелких файлов. Группируйте логику по задаче, для которой она нужна, а не по технологии которую она использует (хуки, стиль и пр.). Постарайтесь следовать принципу "если одни и те же файлы часто меняются совместно при работе над задачей, следует объединить их в один файл"
- Не создавайте более трех вложенных директорий
- В целом, хорошо хранить файлы, которые часто изменяются, совместно ближе друг к другу

## Разное

- В комментариях к коду и сообщениях к коммитам мы используем гибридный язык. Что-то короткое можно писать на английском или русском. Длинное пишем только на русском.
- Функциональность, которая дергает ручки из нового фронтбэка, добавляйте через флаг. Или сначала выкатывайте в одном релизе фронтбэк, а в следующем фронтенд. Выбор подхода на ваше усмотрение.

## Git

- Используйте `merge` только в мастер-ветку
- Используйте `rebase` для синка с основной веткой
- Используйте драфт-реквесты, для незаконченных пулл-реквестов
- Используйте [git rerere](https://git-scm.com/docs/git-rerere) для быстрого решения конфликтов при ребейзе

```bash
git config --global rerere.enabled true
```
