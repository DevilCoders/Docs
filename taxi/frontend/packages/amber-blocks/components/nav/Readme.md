
Ожидает, что в него помещены 

* Теги `<a>`, получающие `className="active"` или `className="amber-link_active"` для активной ссылки. Это совпадает с дефолтным поведением `<NavLink>` из `react-router` и позволяет делать навигационные менюшки для него.
* Или экземпляры `<Link/>` из соседнего компонента.

TODO:

* Добавить поддержку второго уровня навигации

```jsx
<Nav>
    <a href="#link1" className="active">Link1</a>
    <a href="#link2" >Link2</a>
</Nav>
```

```jsx
const Link = require('../link/Link').default;
<Nav>
    <Link url="#link1" active>AmberLink</Link>
    <a href="#link2" >Just a link</a>
</Nav>
```
