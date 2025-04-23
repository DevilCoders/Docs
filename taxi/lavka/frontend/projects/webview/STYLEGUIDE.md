# Правила написания кода

- [Правила написания кода](#правила-написания-кода)
- [Именование переменных](#именование-переменных)
  - [Английский язык](#английский-язык)
  - [Соглашение](#соглашение)
  - [S-I-D](#s-i-d)
  - [Избегайте сокращений](#избегайте-сокращений)
  - [Избегайте дублирования контекста](#избегайте-дублирования-контекста)
  - [Отражайте ожидаемый результат](#отражайте-ожидаемый-результат)
  - [Группировка строк](#группировка-строк)
  - [Именование функций](#именование-функций)
    - [Шаблон A/HC/LC](#шаблон-ahclc)
      - [Action](#action)
        - [`get`](#get)
        - [`set`](#set)
        - [`reset`](#reset)
        - [`fetch`](#fetch)
        - [`remove`](#remove)
        - [`delete`](#delete)
        - [`create`](#create)
        - [`handle`](#handle)
      - [Context](#context)
      - [Prefixes](#prefixes)
        - [`is`](#is)
        - [`has`](#has)
        - [`should`](#should)
        - [`min`/`max`](#minmax)
        - [`prev`/`next`](#prevnext)
  - [Единственное и множественное число](#единственное-и-множественное-число)
- [Используем interface вместо type](#используем-interface-вместо-type)
- [Структура компонент](#структура-компонент)
- [Используем именованные импорты вместо дефолтных](#используем-именованные-импорты-вместо-дефолтных)
      - [Хорошо:](#хорошо)
      - [Плохо:](#плохо)
- [Добавляем название компонента в типы свойств](#добавляем-название-компонента-в-типы-свойств)
      - [Хорошо:](#хорошо-1)
      - [Плохо:](#плохо-1)
- [Используем функциональные компоненты вместо классов](#используем-функциональные-компоненты-вместо-классов)
      - [Хорошо:](#хорошо-2)
      - [Плохо:](#плохо-2)
- [Написание документации](#написание-документации)
      - [Хорошо:](#хорошо-3)
      - [Плохо:](#плохо-3)



# Именование переменных

## Английский язык

Используйте английский язык для именования.

```js
/* Плохо */
const primerNombre = 'Gustavo'
const amigos = ['Kate', 'John']

/* Хорошо */
const firstName = 'Gustavo'
const friends = ['Kate', 'John']
```



## Соглашение

Используйте **только** camelCase для именования переменных

```js
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

```js
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

```js
/* Плохо */
const onItmClk = () => {}

/* Хорошо */
const onItemClick = () => {}
```

## Избегайте дублирования контекста

Имя не должно дублировать контекст в котором оно определено (не относится к экспортированным функциям/переменным). Всегда удаляйте контекст из имени, если это не ухудшает читаемость.

```js
class MenuItem {
  /* Имя метода дублирует контекст ("MenuItem") */
  handleMenuItemClick = (event) => { ... }

  /* Читается нормально `MenuItem.handleClick()` */
  handleClick = (event) => { ... }
}
```

## Отражайте ожидаемый результат

```jsx
/* Плохо */
const isEnabled = itemCount > 3
return <Button disabled={!isEnabled} />

/* Хорошо */
const isDisabled = itemCount <= 3
return <Button disabled={isDisabled} />
```

## Группировка строк

Отдавать предпочтение для слишком простой логики группировать императивные вызовы,
а не разделять кареткой \n

```js
/* Плохо */
setPaymentMethodsLoading(true)

await overlord.loadPaymentMethods()

setPaymentMethodsLoading(false)

/* Хорошо */
setPaymentMethodsLoading(true)
await overlord.loadPaymentMethods()
setPaymentMethodsLoading(false)
```


---

## Именование функций

### Шаблон A/HC/LC

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

#### Action

Глагольная часть имени функции. Описывает, что _делает_ функция.

##### `get`

Получает данные немедленно (геттер).

```js
function getFruitCount() {
  return this.fruits.length
}
```

> См. также [create](#create).

##### `set`

Устанавливает значение переменной.

```js
let fruits = 0

function setFruits(nextFruits) {
  fruits = nextFruits
}

setFruits(5)
console.log(fruits) // 5
```

##### `reset`

Сбрасывает значение переменной к исходному.

```js
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

##### `fetch`

Запрашивает данные, что может занять время (асинхронный запрос).

```js
function fetchPosts(postCount) {
  return fetch('https://api.dev/posts', {...})
}
```

##### `remove`

Удаляет что-то _из_ чего-то.

```js
function removeFilter(filterName, filters) {
  return filters.filter((name) => name !== filterName)
}

const selectedFilters = ['price', 'availability', 'size']
removeFilter('price', selectedFilters)
```

> См. также [delete](#delete).

##### `delete`

Удаляет что-то безвозвратно.

```js
function deletePost(id) {
  return database.find({ id }).delete()
}
```

> См. также [remove](#remove).

##### `create`

Создает новые данные из существующих. Можно согласиться на других вариантах (make или compose).

```js
function createPageUrl(pageName, pageId) {
  return (pageName.toLowerCase() + '-' + pageId)
}
```

> См. также [get](#get).

##### `handle`

Обрабатывает действие. Чаще всего коллбэк.

```js
function handleLinkClick() {
  console.log('Clicked a link!')
}

link.addEventListener('click', handleLinkClick)
```

DOM события onClick, onChange, etc обрабатываются функцией handleClick, handleChange.

```jsx
  <div onClick = {handleClick}></div>
```

Пропсы прокидываемые в компонет в качестве обработчиков именуются через on

```jsx
const Component = ({onClick}) => <div onClick = {onClick}></div>
const Component = ({onClick}) => {
  const handleClick = (e) => {
    onClick(e)
    alert("click")
  }
  return <div onClick = {handleClick}></div>
}
```

---

#### Context

Область с которой оперирует функция.

Функция это чаще всего действие над _чем-либо_. Очень важно указать над чем производится действие или ожидаемый результат.

```js
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

#### Prefixes

Префиксы уточняют имя переменной. Они нечасто используются в названиях функций.

##### `is`

Описывает характеристику или состояние текущего контекста (обычно `boolean`).

```js
const color = 'blue'
const isBlue = color === 'blue' // характеристика
const isPresent = true // состояние

if (isBlue && isPresent) {
  console.log('Blue is present!')
}
```

##### `has`

Описывает существование значение в текущем контексте (обычно `boolean`).

```js
/* Плохо */
const isProductsExist = productsCount > 0
const areProductsPresent = productsCount > 0

/* Хорошо */
const hasProducts = productsCount > 0
```

##### `should`

Отражает возможность выполнения действия при определенном условии (обычно `boolean`).

```js
function shouldUpdateUrl(url, expectedUrl) {
  return url !== expectedUrl
}
```

##### `min`/`max`

Описывает минимальное или максимальное значение.

```js
function renderPosts(posts, minPosts, maxPosts) {
  return posts.slice(0, randomBetween(minPosts, maxPosts))
}
```

##### `prev`/`next`

Описывает предыдущее либо будущее значение состояния в текущем контексте.

```jsx
function fetchPosts() {
  const prevPosts = this.state.posts

  const fetchedPosts = fetch('...')
  const nextPosts = concat(prevPosts, fetchedPosts)

  this.setState({ posts: nextPosts })
}
```

## Единственное и множественное число

Как и префикс, имя переменной может отражать содержит он одно или множество значений.

```js
/* Плохо */
const friends = 'Bob'
const friend = ['Bob', 'Tony', 'Tanya']

/* Хорошо */
const friend = 'Bob'
const friends = ['Bob', 'Tony', 'Tanya']
```


---


# Используем interface вместо type


```ts
/* Плохо */
type UserFormValues = {
  firstName: string
  email: string
}

type BottomSheetProps = {
  close: (result?: unknown) => void
  forceClose: (result?: unknown) => void
}
/* Хорошо */
interface UserFormValues {
  firstName: string
  email: string
}

interface BottomSheetProps {
  close: (result?: unknown) => void
  forceClose: (result?: unknown) => void
}
```


# Структура компонент

Внутри каталога `MyComponent` для компонента определена следующая структура файлов:

```
MyComponent.tsx - код компонента
MyComponent.css.ts - выносим стили в отдельный файл
MyComponent.types.ts - если необходимо, выносим типы в отдельный файл
MyComponent.consts.ts - если необходимо, выносим константы в отдельный файл
MyComponent.context.ts - если есть контекст, делаем его в отдельном файле
/assets - каталог для хранения статики, если есть
index.ts - прокси: импорт и экспорт компонента и других необходимых снаружи вещей
```


# Используем именованные импорты вместо дефолтных

#### Хорошо:
```typescript
export {ComponentA, ComponentB, ComponentC}

export const BeautifulButton = compose(...)(BeautifulButtonComponent)

export {ComponentD} from './ComponentD'
```

#### Плохо:
```typescript
export default {ComponentA, ComponentB, ComponentC}

export default compose(...)(BeautifulButton)

export {ComponentD as default} from './ComponentD'
```


# Добавляем название компонента в типы свойств

#### Хорошо:
```typescript
interface MyComponentProps {...}

interface MyComponentInnerProps {...}
```

#### Плохо:
```typescript
interface OuterProps {...}

interface InnerProps {...}
```


# Используем функциональные компоненты вместо классов

#### Хорошо:
```typescript
const MyComponent = (props: MyComponentInnerProps) => {
  ...
}
```

#### Плохо:
```typescript
class MyComponent extends React.Component<MyComponentInnerProps> {
  render() {...}
}
```


# Написание документации

Для документирования полей внутри типа или методов класса используется схема jsdoc. Над описываемым объектом пишется комментарий в формате `/** Comment */`. Так, IDE при наведении на поле объекта будет показывать подсказку с указанным текстом.

При этом необходимо отделять пустой строкой задокументированные свойства.

#### Хорошо:
```typescript
type MyComponentProps = {
  /** Текст заголовока */
  title: string

  /** Текст описания */
  description: string
}
```

#### Плохо:
```typescript
type MyComponentProps = {
  /* Текст заголовока */
  title: string
  // Текст описания
  description: string
}
```

