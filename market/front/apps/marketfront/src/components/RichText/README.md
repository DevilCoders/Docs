#RichText

Виджет для тайтла и текста с подложкой.
https://shevrov.desktop.marketplace.logrus01ed.beru.ru/brand/lego-igrushki/3732937/nickshevr
### Песочница
```jsx
import RichText from '@self/root/src/components/RichText';

import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

<Helper.Playground
    component={RichText}
    forceUpdate={true}
    defaultValues={{
        title: 'Объединяем данные и технологии',
        text: 'Royal Philips — это ведущая технологическая компания, нацеленная на улучшение качества жизни людей на всех этапах континуума здоровья — от ведения здорового образа жизни, профилактики и ранней диагностики до лечения и ухода.',
        align: 'center',
        theme: 'normal',
        backgroundColor: '#222222',
        backgroundImage: '//img.youtube.com/vi/Iq6CR22Fzv8/hqdefault.jpg',
        height: 300,
    }}
/>
```
