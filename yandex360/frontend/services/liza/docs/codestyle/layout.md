# ns.layout

 1. layout определяется внутри соответствущего модуля в файле `<modulename.layouts.js>`
 2. Для унификации, при объявлении не стоит использовать сокращения, а стоит всегда писать полную форму

```js
ns.layout('page', {
    'app': {
        // хорошо
        'my-view': {
            'my-child-view': {}
        }
    }
});

ns.layout('page', {
    'app': {
        // плохо
        'my-view': true
    }
});

ns.layout('page', {
    'app': {
        // плохо
        'my-view': 'my-child-view'
    }
});
```

 3. Layout объявляется в отдельном файле.
 4. Название лайаута начинается с префикска "layout-".

### Когда дело доходит до patchLayout
`patchLayout` – метод вида, перегрузив который, мы сможем влиять на конечный layout дерева. Если метод используется и возвращает название layout'a,
 то этот layout должен содержать в себе один-единственный бокс.
 Таким образом, получается 3 сущности: вид-обертка, layout и бокс.

 *Пример:*
 Есть вид, который содержит все "замечания" для поля ввода в композе, будь то сообщение об ошибке, сообщение о контакте из внешней сети и т.д.
 Семантически он должен называться `compose-field-notices`.
 Также он использует функциональность `patchLayout`, поэтому чтобы это было сразу понятно, приставим к нему суффикс `-wrapper`, то есть обертка.
 Таким образом, вид – `compose-field-notices-wrapper`.

 Чтобы связать название layout'a, который возвращает `patchLayout`, назовем его также, учитывая пункт 4 выше, то есть `layout-compose-field-notices`.
 Ну а бокс внутри этого layout'a логично назвать с суффиксом `-box`, то есть `compose-field-notices-box`.

 В итоге получаем следующее:
 ```js
 ns.View.define('compose-field-notices-wrapper', {
    methods: {
        patchLayout: function() {
            return 'layout-compose-field-notices';
        }
    }
 });

 ns.layout.define('layout-compose-field-notices', {
    'compose-field-notices-box@': {}
 });
 ```

### `patchLayout` vs `updateByLayout`
Оба метода решают задачу динамического формирования layout-а в приложении.

#### `patchLayout`
`patchLayout` - стандартный механизм, встроенный в `ns.Update`.
Update выполняется до тех пор, пока не будут выполнены все методы `patchLayout` у всех видов, рекурсивно.

#### `updateByLayout`
`updateByLayout` выполняется на более поздней фазе выполнения приложения.
`updateByLayout` используется когда нужно, к примеру, поменять `params` (чтобы виды создавались с использованием изменённых параметров, а не тех, что пришли из урла).

К примеру, у вас ключ вида строится по параметру, которого нет в урле.
В этом случае можно сделать вид-обёртку, который запросит модель, а затем на `ns-view-htmlinit` выполнит `this.updateByLayout('view-inner-layout', modifiedParams, { execFlag: ns.U.EXEC.PARALLEL }).then(callback)`.

Рекомендуется запускать `updateByLayout` с `ns.U.EXEC.PARALLEL` чтобы его не мог отменить глобальный update.

**Внимание, подводные камни:**
- если в процессе `updateByLayout` рендерятся `async` виды - возможны баги.
  К примеру, если async update запускается до глобального, глобальный в итоге может его отменить.
  Подробнее https://github.yandex-team.ru/Daria/liza/issues/950.

