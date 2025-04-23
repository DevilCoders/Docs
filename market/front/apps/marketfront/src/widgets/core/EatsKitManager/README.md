Виджет "Менеджер EatsKit"
======

EatsKit - библиотека, использующаяся для двустороннего взаимодействия мобильных приложений Яндекс Go и страниц,
открытых в вебвью. Данный виджет оборачивает обращения из веб страницы к EatsKit в эпики, позволяя взаимодейстовать
с ним способом, естественным для redux приложений. В дальнейшем также предусматривается обработка запросов из мобильного
приложения на стороне EatsKitManager.

**Вызов методов мобильного приложения из веб страницы.**

Для того, чтобы веб-страница могла вызывать методы приложения, EatsKit встраивает на страницу глобальный объект taxiApp,
вызовы методов которого транслируются приложению. Подробнее об имеющихся методах смотрите на [вики странице протокола](https://wiki.yandex-team.ru/eda/dev/web/Superapp/Protokol-obshhenija-taxApp-edaWebView/).

**Вызов методов веб-страницы из мобильного приложения**

Для того, чтобы EatsKit мог взаимодействовать с веб-страницей, EatsKitManager создает глобальный объект edaWebView.
Подробнее об имеющихся методах смотрите на [вики странице протокола](https://wiki.yandex-team.ru/eda/dev/web/Superapp/Protokol-obshhenija-taxApp-edaWebView/).

**Другие технические детали**

При старте фронт запрашивает у натива через метод taxiApp.call('config', token, {supportedMethods: []}) что умеет натив,
и в последствии использует методы из ответа. (Нужно реализовать)

Между iOS и Android в протоколе есть отличие, что iOS аргументы для методов принимает как объект, а Android, как строку
(в вики описан вариант для iOS)

[Вики страница протокола](https://wiki.yandex-team.ru/eda/dev/web/Superapp/Protokol-obshhenija-taxApp-edaWebView/).

###Пример компонента, использующего EatsKit.

Пример ниже демонстрирует кнопку, которую можно встраивать на страницы, на которые добавлен EatsKitManager.
Данная кнопка посылает команду закрытия окна webview.

####Контейнер
```js
// @flow

import {identity} from 'ambar';
import {type Dispatch} from 'redux';
import {connect} from 'react-redux';

import {TestEatsKit} from '../components/TestEatsKit';

import {
    type RequestHideWebView,
    requestHideWebView,
} from '../actions';

const mapDispatchToProps = (dispatch: Dispatch<RequestHideWebView>) => ({
    requestHideWebView: () => dispatch(requestHideWebView()),
});

export default connect(identity, mapDispatchToProps)(TestEatsKit);
```
####Компонент
```js
// @flow

import React from 'react';
import {Button} from '@self/root/src/uikit/components';

export const TestEatsKit = ({requestHideWebView}: {requestHideWebView: () => void}) => (
    <div>
        <Button onClick={requestHideWebView} text="Вызвать метод requestHideWebView" />
    </div>
);

export default TestEatsKit;
```

