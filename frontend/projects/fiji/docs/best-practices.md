## Критерии хорошего и плохого кода:

### Продуктовый код и технологии
Хорошим тоном является выделение из pull request'а технологических изменений как на уровне проекта, так и на уровне "Сахалина" в отдельный pull request.
Это не только сделает прохождение ревью более быстрым, но и позволит продумывать необходимость технологических изменений в отрыве от продуктового контекста, в разрезе нескольких проектов.

### Общее
* код соответствует нашим стандартам кодирования JS, CSS (пройдены проверки jshint, csslint, jscs; проведён csscomb);
* код задокументирован в соответствии со стандартом JSDoc;
* задокументированы сложные и/или неочевидные места в коде;
* комментарии описывают бизнес-логику;
* для очевидных вещей комментарии не нужны;
* нет дублирования кода, сложных методов, условий и других признаков плохого кода;
* отсутствует хардкодинг переменных;
* переменные выносятся в документированный **config**;
* не нарушается API доступа к внутренним методам блоков;
* функции делают одну задачу, а не несколько;
* чем меньше функция, тем лучше;
* методы и переменные имеют чёткие и понятные названия;
* внутренние методы блока имеют префикс подчёркивания;
* методы блока получают данные либо через переданные аргументы, либо из собственного конфига;
* cначала определены переменные, которым присваивается значение, потом всё остальное;
* переменная имеет говорящее название, без привязки ко времени;
* не определять переменную раньше, чем это требуется;
* eдинообразие в названиях, когда логика разная — названия тоже должны отличаться по смыслу;
* при разработке учитывается скорость выполнения кода;
* используются `if`, а не сложные тернарники и инлайн проверки.

### priv.js
* отделено получение и обработка данных от построения bemjson'a;
* информация о тэгах, вспомогательных обёртках выносится в **bemhtml**;
* всё что можно вычислить на сервере — вычисляем в priv и пробрасываем на клиент окончательный результат в параметрах блока.

### pub.js
* бизнес-логика должна происходить только по **BEM**-событиям, но не **DOM**-событиям.
* блок не слушает **DOM**-события другого блока;
* блок не обращается к внутренним переменным и методам другого блока;
* блок, как правило, не должен искать блок, который находится выше его по **DOM**-дереву;
* для конфига удобно использовать `this.params`, `this.getDefaultParams`;
* метод триггерит не более одного события;
* используется live-инициализация, `live: false` используется в исключительных случаях и подробно документируется;
* отсутствуют вычисления, которые изначально можно выполнить на сервере.

### bemhtml
* внимательно относиться к использованию **applyCtx**, **applyNext**;
* константы передаются в данных, а не определяются в шаблоне.

### css
* не использовать излишний "водопад" для селекторов;

## Примеры
### Хардкодинг и конфиг
**Плохо:**
```
var ratio = Math.max(width / 180, height / 60);
var url = img.thmb_href + '&n=' + (~~data.userInfo.pd > 1 ? '22' : '23');
```

**Хорошо:**
```
var hasRetinaDisplay = ~~data.userInfo.pd > 1;
// 180/60 - максимальная ширина/высота тумба при n=23
config: {
    maxWidth: 180,
    maxHeight: 60,
    thumbParam: hasRetinaDisplay ? '22' : '23'
};
```
> Простые числа менее понятны, чем названия переменных. К тому же они имеют тенденцию к "расползанию" по коду.
При необходимости внести изменения требуются большие усилия, чтобы найти все места, где используются числа, вместо параметров или констант.

### Комментарии
**Плохо:**
```
// Устанавливаем высоту контейнеру
container.style.height = justifier.getColumnsMinHeight() + 'px';
```

**Хорошо:**
```
// Для элементов используется абсолютное позиционирование, поэтому выставляем фиксированную высоту контейнеру.
container.style.height = justifier.getColumnsMinHeight() + 'px';
```
> Необходимо описать бизнес-логику и какой это имеет смысл. То что здесь устанавливается высота — понятно и без комментария.

### Нарушение внутреннего API
**Плохо:**
```
this.otherBlock.setMod('hidden', 'yes');
this.otherBlock.domElem.attr('href', url);
```

**Хорошо:**
```
this.otherBlock.hide();
this.otherBlock.setHref(url);
```
> Влезая во внутренние методы блока, мы не можем гарантировать, что текущее поведение не изменится в будущем.
Например, ссылка будет не внутри самого `domElem`, а одного из элементов блока.
При этом публичное API останется работоспособным.

### Маленькие функции с единственной задачей
**Плохо:**
```
function load() {
    var request = BEM.create('i-request_type_bem', {
        param1: 'value',
        param2: 'value'
    });
    request.block('someBlock', function(response) {
        BEM.DOM.update(this.elem(), response.html);
        this.otherBlock.doSmth();
        this.doSmth();
        this.setMod('done', 'yes');
    });
    request.get();
}
```

**Хорошо:**
```
function loadData() {
    request.block('someBlock', this._onLoadData);
}
function _onLoadData(data) {
    this.updateContent(data.html);
}
function updateContent(html) {
    BEM.DOM.update(this.elem('content'), html);
}
```
> Чем меньше тело функции, тем проще дать ей понятное и однозначное название. Тем легче её отлаживать и тестировать. Она легче будет поддаваться рефакторингу. Заметить side-эффекты будет проще.

### Правильные названия
**Плохо:**
```
function getSize() {
    var getData = someData(),
        url = getSomeUrl();

    return {
        width: getData.width * 5,
        height: getData.height * 10,
        url: url.replace('param', 'value');
    };
}
```

**Хорошо:**
```
functio getThumbSize(img) {
    return {
        width: img.width * this.params.ratio,
        height: img.height * this.params.ratio
    };
}
```

> Название метода должно быть кратким описанием того, что делает функция. Правило работает в двух направлениях. При первичном выборе названия, нужно подобрать точное определение. При рефакторинге или исправлении кода, не стоит дописывать код, который противоречит названию функции.

### Возвращаемые значения

Тип возвращаемого значения функции должен быть ожидаемым.

**Плохо:**
```
function getName() {
    return this._name || false;
}
```

**Хорошо:**
```
function getName() {
    return this._name || '';
}
```

«Пустые» возвращаемые значения по типам:
* `String` → `''`
* `Number` → `NaN`
* `Boolean` → `false`
* `Array` → `[]`
* `Object` → `null`

### Определение переменных
**Плохо:**
```
var container = params.container,
    items,
    containerWithItems = params.containerWithItems,
    containerClassList;
```

**Хорошо:**
```
var container = params.container,
    containerWithItems = params.containerWithItems,
    containerClassList,
    items;
```

### Не определять переменную раньше, чем это требуется
**Плохо:**
```
var serpList = blocks['serp-list__get-all-data'](data),
    isIndex = data.isIndex;

if (isIndex) {
    return false;
}

return serpList;
```

**Хорошо:**
```
var isIndex = data.isIndex,
    serpList;

if (isIndex) {
    return false;
}

serpList = blocks['serp-list__get-all-data'](data);

return serpList;
```
> Записывать данные в переменные необходимо тогда, когда это требуется. Иначе будет выполняться лишняя работа, хотя мы за ранее знаем, что эти данные не нужны.

###Единообразие в названиях
**Плохо:**
```
var heights = [],
    columns = 3;

// Создаем массив, в который потом будем записывать высоту столбца.
for (var i = 0; i < this.columns; i++) {
    heights.push(100 * i);
}
```

**Хорошо:**
```
var heights = [],
    columnCount = 3;

// Создаем массив, в который потом будем записывать высоту столбца.
for (var i = 0; i < columnCount; i++) {
    heights.push(100 * i);
}
```
> При одинаковом формате имён переменных они должны и обрабатываться одинаково.

### Внутренние методы блока
**Плохо:**
```
this.onButtonClick = function() {};
this.updateSomeInternalParam = function() {};
```

*Хорошо:**
```
this._onButtonClick = function() {};
this._updateSomeInternalParam = function() {};
```

### Получение данных внутри методов блока
**Плохо:**
```
this._updateTitle = function() {
    this.elem('title').html(data.someObject.someArray[0]);
}
```

**Хорошо:**
```
this._updateTitle = function(title) {
    this.elem('title').html(title);
}
this._updateTitle = function() {
    this.elem('title').html(this.param.title);
};
```
> У блока должно быть минимизировано количество точек с входными данными. Так проще их валидировать, подготавливать, следить за внешними зависимостями, писать тесты. Внутренние методы блока не должны знать про любые глобальные объекты. Они могут знать либо про аргументы, либо про другие методы и свойства блока.

### Обработка данных и построение bemjson
**Плохо:**
```
blocks['block'] = function(data) {
    var items = data.searchdata.searchtype.arr.slice(0, 15).filter(function(){});
    if (items.bla) {
        items.foo = data.anotherreport.doSmth();
        if (!items.foo) {
             items.baz = data.reportanother.somethingDo();
        }
    }
    return items.map(function(item) {
        block: 'item',
        content: {
            url: data.getUrlForBlock(item.url),
            width: item.foo ? 5 : 10,
            height: item.baz ? blocks['other-block'].getHeight(data.config.smth, item.smth);
        }
    });
}
```

**Хорошо:**
```
blocks['block'] = function() {

    var items = this.prepareItems(data.searchdata);

    return this.getBEMJSON(items);

};

blocks['block'].prepareItems = function(items) {
    return items.map(function(item) {
        item.value = ...;
        item.anotherValue = ...;
    });
}

blocks['block'].getBEMJSON = function(items) {
    return items.map(function(item) {
        return {
            block: 'item',
            content: item.value
        }
    });
};
```
> Это как отделять код от шаблонов. Для удобства тестирования, чтения и отладки кода, гораздо удобней выносить получение данных и построение BEMJSON-дерева по этим данным в разные методы. Тогда код становится более простым и понятным.

### Разделение *priv.js* и *bemhtml*
**Плохо:**
```
blocks['block'].getBEMJSON = function(items) {
    return {
        tag: 'span',
        content: {
            block: 'block',
            content: [
                { elem: 'decorate-arrow' },
                { elem: 'business-logic' }
                { elem: 'decorate-shadow' }
            ]
        }
    };
};
```

**Хорошо:**
```
blocks['block'].getBEMJSON = function(items) {
    return {
        block: 'block',
        content: {
            elem: 'business-logic'
        }
    };
};
```

### События клиентских блоков
**Плохо:**
```this.bindTo(this.elem('button'), 'click', this.doSomeBusinessLogic);```

**Хорошо:**
```
this.bindTo(this.elem('button'), 'click', this._onClick);
this._onClick = function(e) {
    if (e.data.value && !this.hasMod('disabled', 'yes') {
        this.trigger('buttonClick');
    }
}
this.on('buttonClick', this._onButtonClick);
this._onButtonClick = function() {
    this.doSomeBusinesLogic(this.getSomeInfoFromButton());
}
```

### Блок не слушает события другого блока
**Плохо:**
```
this.block.bindTo('click', this.doSmth);
```

**Хорошо:**
```
this.block.on('someClick', this._onBlockSomeClick');
```

### Блок не обращается к внутренним переменным другого блока
**Плохо:**
```
this.block.elem('title').attr('title', 'value');
```

**Хорошо:**
```
this.block.setTitle('title');
```

### Связывание блоков
```
<div class="block another-block">
   <div class="child-block">
   </div>
   <div class="child-another-block">
       <div class="child-child-block">
       </div>
   </div>
</div>
```
**Плохо:**
```
// child-child-block
this.findOutside('block').findInside('child-block').doSmth();
```

**Хорошо:**
```
// child-child-block
this.trigger('event');

// block
this.findBlockInside('child-child-block').on('event', function() {
   this.findBlockInside('child-block').doSmth();
})
BEM.blocks['child-child-block'].on(this.domElem, 'event', function() {};
```

**Плохо:**
```
// child-child-block
this.findBlockOutside('block').doSmth();
```

**Хорошо:**
```
// block
this.findBlockInside('child-child-block').doSmth();

// или

// child-child-block
this.trigger('someEvent');
// block
this.childBlock.on('someEvent, function() {});
```

### Параметры
**Плохо:**
```
BEM.DOM.decl({
    someValue: 5,
    anotherValue: 10
})
```

**Хорошо:**
```
BEM.DOM.decl({
    getDefaultParams: function() {
        return {
           value: 5,
           anotherValue: 10
        }
    }
});
```

### При разработке учитывается скорость выполнения кода
**_.assign(dest, source) vs dest.a = source.a**

```
assign x 505,509 ops/sec ±0.86% (87 runs sampled)
plain js x 35,184,739 ops/sec ±0.76% (85 runs sampled)
Fastest is plain js
```

(https://paste.yandex-team.ru/154940)

> Cомнительный код прогоняем через JSPerf, прикладываем в пулл как можно улучшить.
