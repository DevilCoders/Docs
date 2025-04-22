## Как устроен роутинг
### Как сделать во вьюхе переход на другую страницу по onClick
Манипуляции с урлом производятся модулем `utils/history` (обертка над [history](https://www.npmjs.com/package/history)).

```
import * as history from 'utils/history';
...
history.push({pathname: '/'});
history.goBack();

```
В `history` есть метод `.push()` и `extend()`, которые осуществляют переход на страницу. Отличие заключается в сохранении/мерже query-параметров.
Так, находясь в `/index?foo=bar`, `history.push({pathname: '/library', query: {type: 'color'}});` удалит все существующие параметры и на выходе окажется `/library?type=color`, а `history.extend({pathname: '/library', query: {type: 'color'}});` сохранит их `/library?foo=bar&type=color`.

Метод `.goBack()` для возврата на предыдущую страницу.

```
history.goBack();
```
### Как приложение восстанавливает состояние после перезагрузки страницы
`RootStore` подписан на изменение истории и решает, что должно загрузиться на той или иной странице.
```
function afterCreate(): void {
    onHistoryChange(history.location);

    history.listen(onHistoryChange);
}

```

Чтобы корректно востановить данные о редактируемом дизайне после перезагрузки, урл страницы должен содержать необходимые get-параметры.
Например:

```
https://cartograph.yandex-team.ru/studio?service=SERVICE_NAME&branch=BRANCH_ID&revision=REVISION_ID
```

Данные о SERVICE_NAME, BRANCH_ID, REVISION_ID позволят сделать запрос на редактируемый бандл.

```
const bundle = await factoryProvider
    .getBundle({revisionId: self.revisionId});

self.setResponseBundle(bundle);
```
