# Быстрый старт на React

В данном разделе описано, как начать использовать Баобаб в вашем проекте на React.

Так же вам может потребоваться информация о настройке [логирования сервиса баобабом и подключение АБТ](https://wiki.yandex-team.ru/baobab/log-your-service/)

### Подключить зависимости
В package.json проекта добавить зависимость
```bash
npm install --save @yandex-int/react-baobab-logger
```

### Создать корневой элемент
Выберите React-компонент, который будет корнем вашего Баобаб-дерева.
Обычно это основной компонент вашего приложения.
Оберните его HOC'ом `withBaobabRoot`.

```typescript jsx
import React from 'react'; 
import { Logger, Sender, withBaobabRoot } from '@yandex-int/react-baobab-logger';

interface IYourRootComponentProps {
    // Описание props...
}

class YourRootComponentBase extends React.Component<IYourRootComponentProps> {
    // Реализация...
}

export const YourRootComponent = withBaobabRoot<IYourRootComponentProps>(
    {
        name: '$page',
        attrs: {
            service: 'ugc',
            ui: 'desktop',
        }
    }, // Описание корневой ноды и её атрибутов
    Logger, // Класс-конструктор Логгера, для управлением логирования (если подходит стандартный -- используй его)
    Sender, // Класс-конструктор Сендера, для управлением отправки логов на сервер (если подходит стандартный -- используй его)
    logger => {}, // Колбек, который возвращает инстанс Логгера после инициализации (необязательный параметр)
)(YourRootComponentBase);
```
После этого у вас готов корневой компонент для логирования.
Всё, что будет внутри него, будет логироваться.

### Сформировать начальный стейт
Для инициализации Баобаб и начала логирования требуется задать начальные данные.
Перед рендером React компонентов сформируйте объект на сервере, который будет передан в корневой компонент.

```typescript
import { getBaobabInitState } from '@yandex-int/react-baobab-logger';

const baobabState = getBaobabInitState({
    reqId: '1569...-12681', // reqid запроса
    service: 'ugc', // Название вашего сервиса
    table: 'ugc', // Название таблицы, куда будет писаться лог. Если не указан, то значение будет взято из service
    pageUrl: 'yandex.ru/ugcpub', // Расположение вашего сервиса
    slots: ['146820,0,40', '102711,0,5'], // Данные о проводимых экспериментах (необязательный параметр)
});
```

### Использование в коде
Передайте стейт, сформированный в предыдущем пункте в корневой компонент.

```typescript jsx
export const App = (
    <YourRootComponent
        logNode={{ attrs: { ui: 'touch' } }} // Через logNode можно переопределить параметры
        baobab={baobabState} // Задаём начальный стейт
    />
);
```

### Отладки и проверки
> TODO: https://st.yandex-team.ru/SERP-98463

### Готово!
После этого ваш сервис должен начать логирование.
