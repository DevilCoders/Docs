#b-date-range-picker#

##Описание##
Блок для выбора календарного периода

###Автор###
[skywhale](https://staff.yandex-team.ru/skywhale)

###Где используется###
* на страницах статистики `b-statistics-form`
 
  ![super-calendar](https://jing.yandex-team.ru/files/skywhale/2015-11-02_13-17-57.png)
  
* на странице «Расчет потенциала клиента» `b-new-potential-report`

  ![b-new-potential-report](https://jing.yandex-team.ru/files/skywhale/2015-11-02_13-16-22.png)

   
###Взаимодействие с другими блоками###

####Календарь#####
По умолчанию использует `b-date-input`, в модификаторе `type: super` использует `super-calendar` [календарь метрики](https://github.yandex-team.ru/Metrika/calendar/).
В обоих случаях слушает `change` на календарях и приводит дату к необходимому формату.

####Элементы выбора шаблонных периодов####
По умолчанию использует блоки `link`, в модификаторе `type: super` использует `b-chooser`. В `js` параметрах соответствующих элементов хранятся данные начала и конца периода.
    
##Как пользоваться и расширять##
####Параметры####

```
{Object} start - информация о начале периода  
{String} start.value - дата начала в формате YYYY-MM-DD  
{String} [start.name] - name для скрытого инпута  
{Object} [start.limits] - ограничения календаря  
{String} [start.limits.earlier] - минимальная дата в формате YYYY-MM-DD  
{String} [start.limits.later] - максимальная дата в формате YYYY-MM-DD

{Object} finish - информация о конце периода  
{String} finish.value - дата конца в формате YYYY-MM-DD  
{String} [finish.name] - name для скрытого инпута  
{Object} [finish.limits] - ограничения календаря  
{String} [finish.limits.earlier] - минимальная дата в формате YYYY-MM-DD  
{String} [finish.limits.later] - максимальная дата в формате YYYY-MM-DD  

{Object[]} [ranges] - массив шаблоннов  
{String} ranges.title - название для пользователя  
{Number|Object} ranges.start - число дней от текущей даты, или объект где название ключа это величина(day|years|period... [подробнее](http://momentjs.com/docs/#/manipulating/add)). Для величины period сдвигается дата на один день, что бы периоды не пересекались.
{Number|Object} ranges.finish - число дней от текущей даты, или объект где название ключа это величина(day|years|period... [подробнее](http://momentjs.com/docs/#/manipulating/add)). Для величины period сдвигается дата на один день, что бы периоды не пересекались.
{String} [ranges.dependId] - id календаря относительно которого будет считаться ranges.start и ranges.finish

{Object[]} [history] - массив истории пользователя
{String} ranges.title - название для пользователя
{String} ranges.start - дата начала в формате YYYY-MM-DD
{String} ranges.finish - дата конца в формате YYYY-MM-DD

{String} [minDate] - минимальное разрешенное значение в формате YYYY-MM-DD

{String} [maxDate] - максимальное разрешенное значение в формате YYYY-MM-DD

{String} [dateFormat] - формат в котором блок будет отдавать значение

{String} [viewFormat] - формат даты для пользователя, не совместим с модификаторм type: super

{Array|Object} [calendarMix] - микс на календарь, не совместим с модификаторм type: super
```

####Основные методы####

* `getRange` - возвращает текущие значение диапазона
* `setRange` - устанавливает новое значение диапазона

Смотри jsdoc: 

* `b-date-range-picker.js`
* `b-date-range-picker_type_super.js`
* `b-date-range-picker.utils.js`


##Roadmap & known issues##
Позиционировании календаря `type: super`. Сейчас календарь умеет открываться по середине страницы или слева относительно `owner`, `super-calendar` сложно модифицировать.

##Пример##

```
{
    block: 'b-date-range-picker',
    id: 'calendar-a',
    start: '2014-11-05',
    finish: '2014-11-20',
    ranges: [
        { title: iget('вчера'), start: -1, finish: -1 },
        { title: iget('7 дней'), start: -7, finish: 0 }
    ],
    minDate: '2014-11-05',
    maxDate: '2014-12-05',
    dateFormat: 'YYYY-MM-DD',
    viewFormat: 'DD MMM YYYY'
}
```

```
{
    block: 'b-date-range-picker',
    mods: { type: 'super' },
    id: 'calendar-b',
    start: '2015-11-05',
    finish: '2015-11-20',
    ranges: [
        {
            title: iget('предыдущий период'),
            start: { period: -1 },
            finish: { period: -1 },
            dependId: 'calendar-a'
        }
    ]
}
```
