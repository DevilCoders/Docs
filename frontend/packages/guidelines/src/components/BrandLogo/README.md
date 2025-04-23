Компонент для отображения логотипов.

### Свойства компонента BrandLogo

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `absolute` `acado` `accion` ...  | Имя иконки |
| `size` | `s` `m` `l` `xl` | Размер |

```jsx
<div>
	<BrandLogo name='allo-inkognito' size='s' />
	<BrandLogo name='allo-inkognito' size='m' />
	<BrandLogo name='allo-inkognito' size='l' />
	<BrandLogo name='allo-inkognito' size='xl' />
</div>
```

#### Список всех лого
```js noeditor
const AllBrandLogos = require('../../styleguide/components/AllBrandLogos').default;

<AllBrandLogos />
```
