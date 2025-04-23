# DropdownContainer

Выпадающий контейнер для отображения произвольного контента.

Компонент и попап можно стилизовать при использовании (см. параметры `className`, `buttonClassName` и `popupClassName`).

Умеет закрываться по клику вне зоны контейнера (см. Пример 2). Outline по фокусу, к сожалению, скрыт намерено,
чтобы попасть в существующий вид блока из продакшена.

## Пример использования

### 1. Базовый пример
```jsx

<DropdownContainer
    placeholder="Выберите нужные параметры"
    onOpen={() => {console.log('Пример 1: ', 'open')}}
    onClose={() => {console.log('Пример 1: ', 'close')}}
>
    <p style={{textAlign: 'center'}}>произвольный контент</p>
</DropdownContainer>
```
### 2. Пример с тайтлом и автозакрытием
```jsx

<DropdownContainer
    autoclosable
    placeholder="Выберите нужные параметры"
    title="КОЛИЧЕСТВО ЯДЕР ПРОЦЕССОРАПРОЦЕССОР (ПОДРОБНО)ПРОЦЕССОР И ЕЩЕ 14"
    onOpen={() => {console.log('Пример 2: ', 'open')}}
    onClose={() => {console.log('Пример 2: ', 'close')}}
>
    <p style={{textAlign: 'center'}}>произвольный контент</p>
</DropdownContainer>
```

### 3. Пример рендера открытого контента
Если компонент рендериться с открытым попатом, но на его контрол открытия (button) будет установлен автофокус.
Это нужно для того, чтобы пользователь (в том числе и слабовидящий) мог закрыть попап с клавиатуры: `space` или `enter` .
```jsx

<DropdownContainer
    placeholder="Выберите нужные параметры"
    title="КОЛИЧЕСТВО ЯДЕР ПРОЦЕССОРАПРОЦЕССОР (ПОДРОБНО)ПРОЦЕССОР И ЕЩЕ 14"
    isOpen={true}
    onOpen={() => {console.log('Пример 3: ', 'open')}}
    onClose={() => {console.log('Пример 3: ', 'close')}}
>
    <p style={{textAlign: 'center'}}>произвольный контент</p>
</DropdownContainer>
```
