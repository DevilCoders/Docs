r104847
Блок подготовки данных для таблиц статистики кампании.

### p-campaign-stat ###

В p-campaign-stat для отображения статистики используется блок b-campaign-stat-data
На вход блоку передаются данные статистические данные кампании.
Например для любой вкладки статистики, в p-campaign-stat.bemtree.xjst передается:

    {
        block: 'b-campaign-stat-data',
        campaign: data.campaign,
        tasesnum: data.tasesnum,
        sesnumForWeek: data.sesnum_for_week,
        directya: data.directya,
        fraudClicks: data.fraud_clicks,
        form: data.FORM,
        cid: data.cid,
        noDataFound: data.no_data_found,
        group: data.group,
        spec: data.spec,
        all: data.all,
        fraudGiftClicks: data.fraud_gift_clicks,
        avGrouping: data.av_grouping,
        uidUrl: data.uid_url,
        period: iget('с') + ' ' + data.d1 + '.' + data.m1 + '.' + data.y1 + ' ' +
           iget('по') + ' ' + data.d2 + '.' + data.m2 + '.' + data.y2
    }

специфические данные для каждой вкладки могут быть доопределены/переопределены в модификаторах p-campaign-stat.
Например для вкладки "статистика по дням"
переопределяется p-campaign-stat__stat-data (элемент который формирует блок b-campaign-stat-data):

    elem stat-data, default: {
        var data = this.data;

        return applyCtx(this._.extend(
            applyNext(),
            {
                mods: { type: 'detail' },
                bannersOnPage: data.banners_on_page,
                banners: data.banners,
                campstat: data.campstat,
                plotGroup: data.plot_group,
                b: data.b
            }));
    }

### b-campaign-stat-data ###

В моде default b-campaign-stat-data формируются поля для использования внутри блока,
важно что в this.campStatCtx - хранится весь переданный в блок контекст.

В моде content для любой вкладки статистики формируются 2 таблички.
 1) total-table
 2) detailed-table
Каждая из которых представляет собой объект с массивом строк. Объект на странице превратится в тег tbody.
Обе таблички мержатся и передаются в виде контента в b-stat-table
На выходе из моды content блок b-campaign-stat-data возвращает

    {
        block: 'b-stat-table',
        mods: mods,
        content: [ // массив табличек
            {
                rows: [
                    {
                        cols: [  //массив ячеек
                            каждая ячейка объект { content: 'bla', someAttrs: ... }
                        ]
                    },
                    ...
                ],
                someAttrs: ...
            },
            ...
        ]
    }

### b-campaign-stat-data__total-table ###

b-campaign-stat-data__total-table - общая табличка для всех вкладок статистики.
Состоит из 4 элементов
 1)total-table-head
 2)total-table-common-cells
 3)total-table-metrics-cells
 4)total-table-foot-elem-name ( по умолчанию возвращает 'total-table-foot' ) //todo убрать этот элемент и зашить отличия в модификатор

total-table-common-cells и total-table-metrics-cells ячейки одной.
Разделение нужно для случая когда мы не отрисовываем ячейки метрики


### b-campaign-stat-data__detailed-table ###

b-campaign-stat-data__detailed-table - это все таблички которые под b-campaign-stat-data__total-table
В зависимости от модификатора b-campaign-stat-data__detailed-table может состоять
из таблиц (тыблицы) которые специфичны для конкретной вкладки статистики.
Например:
    1) для вкладки "статистика по дням" b-campaign-stat-data__detailed-table состоит из
        a)campaign-summary-table
        b)banners-table
        Каждая из этих таблиц формирует специфичный для себя заголовок и вызывает элемент table-parts
    2) для вкладки "мастер отчетов"  b-campaign-stat-data__detailed-table_type_custom
       просто вызываются table-head и row в которые передаются подготовленные данные


### b-campaign-stat-data__table-parts ###

Элемент table-parts в цикле вызывает формирование элементов table-head, table-body, table-foot и пробрасывает в каждый
данные статистики statData

пример использования table-parts

    applyCtx({
        elem: 'table-parts',
        statData: banner,
        cellsItems: [{ // cellsItems
            id: 'sorting',
            title: iget('Дата')
        }]
    });

на вход элементу передаем
 1) statData - объект содержащий статистические данные (банер, кампания)
 2) cellsItems - необязательное поле. Это поле является описанием кастомных (специфичных для конкретной вкладки) колонок.
    В него можно передать масив объектов содержащих id (поле по которому будет происходить сортировка) и
    title (локализированное название колонки)

на выходе получим
    [
        {
            rows: [
                {
                    cols: [
                        { content: ... },
                        { content: ... }
                    ]
                },
                ...
            ]
        }
    ]


### b-campaign-stat-data__table-head ###

В table-head формируется заголовок таблицы (общие поля и поля метрики).
Если есть необходимость добавить поля, например вкладки "мастер отчетов",
то небходимо в контекст пробросить массив cellsItems с id поля и именем

    applyCtx({
        elem: 'table-head',
        cellsItems: [
            { id: 'mySpecIdForSpecialTab', name: 'specName', colspan: 13 }
        ]
    })

### b-campaign-stat-data__table-body ###

Подготавливает, сортирует массив данных для строки.
Элемент внутри использует b-campaign-stat-data__row
которому в контексте передает rowData и additionalFields (при необходимости)
additionalFields это объект хранящий информацию о полях специфичных для конкретной вкладки
Например если нам нужно добавить поля specField и bla то

    additionalFields = {
        names: ['specField', 'bla'],
        elemName: 'additional-fields-cells-formatter' // произвольный элемент
    }

additional-fields-cells-formatter - это имя элемента который займется форматированием специфических полей
Таким образом если нужно добавить поле (или несколько) в табличку то необходимо указать его имя
и элемент который отформатирует данные этого поля. Элемент-обработчик нужно написать для каждого конкретного случая.

### b-campaign-stat-data__row ###

формирует массив ячеек строки

    applyCtx({
        elem: 'row',
        rowData: data,
        additionalFields: {
            names: ['name1', 'name2'],
            elemName: 'additional-fields-formatter'
        }
    })

на вход передаем
  rowData - данные для строки (например: данные статистики за один день)
  additionalFields - объект хранящий информацию о полях(колонках) специфичных для конкретной вкладки
  additionalFields.names - имена специфичных для вкладки полей
  additionalFields.elemName - обработчик добавляемых полей


### Краткий алгоритм для старта при создании новой страницы статистики ###

Для специального форматирования таблицы нужно создать модификатор элемента detailed-table
по образцу, дополнив и организовав согласно задаче:


    block b-campaign-stat-data, elem detailed-table, elemMod type TYPE, default: {
        // приходится "растягивать" первую колонку в зависимости от количества площадок
        var firstCellColspan = this.targetsLength + 1,
            dataArray = this.campStatCtx.dataArray,
            // используем общий для всех заголовок
            headRows = applyCtx({
                elem: 'table-head',
                // при необходимости задаём кастомные колонки
                cellsItems: [
                    {
                        id: 'sorting',
                        title: iget('Позиция'),
                        hideTargets: true,
                        colspan: firstCellColspan
                    }
                ]
            }),
            // преобразуем данные статистики в список строк для таблицы
            // можно вынести в специализированный элемент по примеру elem: 'table-head'
            bodyRows = applyCtx(dataArray.map(function(rowData) {
                return { elem: 'row', rowData: rowData };
            }));

        return [
            // это станет tbody заголовка
            {
                rows: headRows
            },
            // а это - tbody основной таблицы со статистикой
            {
                rows: bodyRows.map(function(cols, index) {
                    var rowData = dataArray[index];

                    // добавляем в начало значения для ячеек кастомных колонок
                    cols.unshift(
                        {
                            content: index + 1,
                            attrs: { colspan: firstCellColspan }
                        });

                    return { cols: cols, isHoliday: rowData.holiday };
                })
            }
        ]
    }


При этом, данные должны быть переданы в блок b-campaign-stat-data через параметр dataArray как список, каждый элемент
которого является объектом, содержащим данные о статистике:

    {
        block: 'b-campaign-stat-data',
        mods: { type: TYPE },
        dataArray: [...objects...]
        ....
    }

Все остальные данные, требуемые частными случаями так же могут быть переданы через контект и будут доступны
в переменной this.campStatCtx.

Вики - https://wiki.yandex-team.ru/adv-interfaces/direct/statistics-page-guide

# author
* Timur Izmajlov kabzon@yandex-team.ru
