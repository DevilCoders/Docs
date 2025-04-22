Компонент для отображения логотипов. [BrandLogo](#!/BrandLogo) — для внешних паратнёров, а ServiceLogo — для внутренних сервисов.
В интерфейсе они могут находится рядом и вставать в общую линейку.
Комуникационные дизайнера Яндекса показали наработки, как будет развиваться визуальная часть логотипов внутренних сервисов, будет добавляться пачка новых модификаторов. А логотипы партнёров строго оформляются под указанный гайд.

В связи с этим логотипы внутренних сервисов вынесли в отдельный блок, чтобы не блокировать его дальнейшее развитие.

### Свойства компонента ServiceLogo

| Название | Значения | Описание |
| -------- | -------- | -------- |
| `name` | `afisha`, ... | Имя логотипа |
| `size` | `s` `m` `l` `xl` | Размер |

```jsx
<React.Fragment>
	<ServiceLogo name='afisha' size='s' />
	<ServiceLogo name='afisha' size='m' />
	<ServiceLogo name='afisha' size='l' />
	<ServiceLogo name='afisha' size='xl' />
</React.Fragment>
```

### Добавление логотипа

Для того, чтобы добавить логотип сервиса, нужно добавить его в директорию `common.blocks/service-logo`. При коммите запустится таск `generate:service-logos-config`.

### Список всех логотипов
```js noeditor
const AllServiceLogos = require('../../styleguide/components/AllServiceLogos').default;

<AllServiceLogos />
```
