
## Тестирвование эпиков

Задача эпиков - генерировать action'ы в ответ на другие action'ы

Не смотря на то, что эпики неявно тестируются во время взаимодействия с view виджета, тем не менее вы можете
протестировать эпик в отрыве от виджета.

Эпики apiary-виджетов параметризируются объектом с данными о параметрах виджета и коллекциями.

Для воспроизведения этого поведения testament содержит хелпер для запуска эпиков.

__epics.spec.js:__

```js
import createEpicExecutor from '@yandex-market/testament/platform/apiary/epicExecutor';

const callEpic = createEpicExecutor(widgetData, collections)(epic);

describe('expConfirm', () => {
    it('reload должен приводить к перезагрузке страницы', async () => {
        const action = await callEpic(expConfirm({ reload: true })).toPromise();

        expect(action).toMatchSnapshot();
        expect(window.location.reload).toHaveBeenCalled();
    });
});
```

В примере выше мы покрываем результат вызова эпика снапошотом и убеждаемся в том,
что `window.location.reload` был вызван
