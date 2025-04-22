===b-model-block===
модель с DOM-представлением

При инициализации (_js_inited) блока, данные из полей формы попадают в js представление модели
Также обеспечивает синхронизацию данных между DOM и js представлениями

При большом колличестве блоков, падает производительность (пример - страница кампании)

При декларации наследника %%b-model-block%% должен присутствовать метод initConsts с определением пути и имени модели. 
%%(javascript)
onSetMod: {
    js: function() {
        ...
    }
},

initConsts: function() {
    this._modelPath = 'campaign';
    this._modelName = 'b-new-block';
}
%%
На данный момент вываливается ошибка, если этого не сделать.

Поля модели именуем через "_", а соответствующий этому полю элемент формы будет являться элементом блока, с именем через "-"
%%(javascript)
BEM.blocks['b-model'].register('b-my-block', {
    fields: {
        lala_topola: {value: '', type: 'string'}
    }
});
%%
%%(html)

<input type="hidden" class="b-my-block__lala-topola" value="bla" name="<<произвольное имя, для общения с сервером>>" />
%%
