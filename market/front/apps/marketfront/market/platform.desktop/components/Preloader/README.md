# Preloader

Спиннер загрузки с паранджой над контентом.

Может принимать кастомные классы на корневому контейнер с паранджой.

Родительский элемент, который должен перекрывать паранджой, должен быть с `position: relative`.

Пример использования:
```jsx
<div style={{height: '100px', position: 'relative'}}>
    <div>Какой-нибудь контент</div>
    <Preloader progress={true} />
</div>

```
