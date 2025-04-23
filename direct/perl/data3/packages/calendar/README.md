## Super-Calendar

Блок реализующий календарь с возможностью выбора периода.

### Установка
1. Добавляем в bower.json зависимость
```
{
    "name": "metrika-global",
    "version": "0.1",
    "dependencies": {
        "romochka": "git://github.yandex-team.ru/lego/romochka.git#2.10.20",
        "super-calendar": "git://github.yandex-team.ru/Metrika/calendar#0.0.2"
    }
}
```
(ромочка тоже нужна). Также не забываем исправить коммит на последнюю версию.

2. Добавляем новый уровень переопределения в сборку 
(bower_components/super-calendar/blocks)

3. Локализируем у себя в проекте (пока в танкере нет отдельного проекта для супер-календаря)
```
(function () {
    var __base = SuperCalendar.prototype.locale.common;
    SuperCalendar.prototype.locale = {
        common: function () {
            this._keysets = {
                title: BEM.I18N('super-calendar', 'title'),
                selectWeek: BEM.I18N('super-calendar', 'choose-week'),
                now: BEM.I18N('super-calendar', 'today'),
                selectionError: BEM.I18N('super-calendar', 'selection-error'),
                submit: {
                    show: BEM.I18N('super-calendar', 'submit-show'),
                    ok: BEM.I18N('super-calendar', 'submit-ok'),
                    select: BEM.I18N('super-calendar', 'submit-select')
                },
                collapse: BEM.I18N('super-calendar', 'collapse'),
                expand: BEM.I18N('super-calendar', 'expand'),
                close: BEM.I18N('super-calendar', 'close'),
                move: BEM.I18N('super-calendar', 'move')
            };
            return __base.apply(this, arguments);
        }
    };
})();
```
### Зависимости:

* >= jQuery 1.8.2
* $.browser (jQuery 2.0)
* jquery.mousewheel.js
* i-tanker (git://github.yandex-team.ru/lego/romochka.git#2.10.20)

### Пример:
```
var sc = new SuperCalendar({
    markedDate: {
        '2010-09-11': 'Hello world!',
        '2011-11-12': 'Example'
    }, // Помечать определенные даты
    title: 'test' // Ключ тайтла из локали для календаря, false если тайтл не нужно отображать
    disabledDates: ['30.01.2008', '01.04.2009', '02.04.2009'] // Заблокированные для выбора даты, отключает selectorWeeks и selectorMonths
    selectorWeeks: true, // Быстрый выбор недели
    selectorMonths: true, // Быстрый выбор месяца
    resize: true, // Возможность изменять размер календаря
    animation: true, // Анимация, в IE не поддерживается
    speedAnimation: 'fast' // Скорость анимации: slow, normal, fast
    minYear: 2008, // Ниже этого года дату не отображать
    maxYear: 2013, // Выше этого года дату не отображать
    minDate: '20.01.2008', // Минимальная дата, всё что младше затеняется серым текстом и не выбирается
    maxDate: '01.05.2009', // Максимальная дата, всё что старше затеняется серым текстом и не выбирается
    minGrayDate: '30.01.2008', // Всё что младше затеняется серым текстом
    maxGrayDate: '01.04.2009', // Всё что старше затеняется серым текстом
    shadow: false, // Затеняющая весь контент тень при открытии календаря
    opacityShadow: 0.2 // Прозрачность тени
    center: true, // Центровка по ширине окна браузера
    submitButton: 'show', // Название кнопки выбора даты
    mousewheel: true, // Поддержка колесика мышки для изменение даты в календаре
    buttons: {
        close: true, // Кнопка закрытия календаря
        maximize: true // Кнопка раскрытия календаря на весь экран
    },
    touch: false, // Поддержка тач-устройств (таскание окна и изменение размеров). Указывать true необходимо только для тач-устройств (iPhone, iPad, Android)
    period: period, // Выбранный период
    onSelect: onSelect, // callback, при выборе даты получает дату, нажатую кнопку и отформатированную дату
    calledElement: calledElement, // Элемент при клике, вызывающий календарь
    positionElement: positionElement // Календарь позиционируется относительно этого элемента
});   
```
```
<div class="super-calendar__selector g-js" onclick="return {'name': 'super-calendar__selector', minYear: 2008, minDate: '01.01.2008'}">Отчетный период: <button><span></span><i class="super-calendar__selector-i"></i></button>
    <input name="date1" type="hidden" value="" />
    <input name="date2" type="hidden" value="" />
</div>
```


