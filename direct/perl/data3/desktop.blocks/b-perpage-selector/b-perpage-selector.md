#Блок выбора количества элементов на странице#

Служит для вывода селекта вариантов количества элементов на странице

Содержимого блока по умолчанию нет, нужно добавлять в content элемент
`{ elem: 'pages-selector' }`

## Пример ##

`{
    block: 'b-perpage-selector',
    perPageParamName: 'objects_on_page',
    pages: {
        10: '10',
        30: '30',
        50: '50',
        100: '100',
        all: iget('Все')
    },
    url: u.getUrl(data.cmd, u.getUrlParams(['cmd', 'objects_on_page', 'page'])),
    onpage: data.FORM.objects_on_page,
    content: {
        elem: 'text',
        content: iget('Показывать %{pagesSelector} заявок на странице', {
            pagesSelector: { elem: 'pages-selector' }
        })
    }
}`
