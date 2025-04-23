# Breadcrumbs

Хлебные крошки

Может отображаться с разными иконками-разделителями, которые определяются следующими параметрами:
* iconName - список имен для иконок смотреть в Левитане, по умолчанию 'corner-right'
* iconColor -  названия цветов смотреть в Левитане, по умолчанию 'gray300'

Эти параметры передаются в компонент Icon. Подробнее о нем по ссылке
https://pages.github.yandex-team.ru/market/levitan-annex/desktop/#/Levitan%20Gui?id=icon

Параметр theme передается в компонент Link

Параметр items обязателен, содержит крошки, может быть сгенерирован хелпером extractBreadcrumbs
из @self/project/src/entities/breadcrumb/helpers

Пример использования:
```jsx
import {Provider} from 'react-redux';
import {createStore} from 'redux';
const store = createStore(() => ({
    collections: {},
}));

const items = [
    {
        text: 'Электроника',
        url: '/catalog--elektronika-v-novosibirske/54440?hid=198119'
    },
    {
        text: 'Аудио- и видеотехника',
        url: '/catalog--audio-i-videotekhnika-v-novosibirske/58428?hid=10599873'
    },
];
<Provider store={store}>
    <Breadcrumbs theme="light" items={items} iconName="bullet" iconColor="gray600" />
</Provider>
```
