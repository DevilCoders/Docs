Ссылка
```jsx
<Link url="http://lenta.ru">Текст ссылки</Link>
```

Ссылка с иконкой
```jsx
const Taxicar = require('../icon/Taxicar').default;
<Link url="http://microsoft.ru"><Taxicar color="#4D40F9"/> Бывает и такое</Link>
```

__Deprecated__ - используй в таких случаях Nav. Ссылки в шапке
```jsx
<Link theme="header-nav" active>Заказ такси</Link>
<Link theme="header-nav" url="http://yandex.ru">Приложение</Link>
<Link theme="header-nav" url="http://yandex.ru">Поддержка</Link>
<Link theme="header-nav" url="http://yandex.ru">Бизнесу</Link>
<Link theme="header-nav" url="http://yandex.ru">Стать водителем</Link>
```
