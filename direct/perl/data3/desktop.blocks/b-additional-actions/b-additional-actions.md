#b-additional-actions#

Блок для вывода ссылок в нижней части страниц Мои кампании (p-campaigns),
мои клиенты для агентств (p-clients) и менеджеров (p-manager-my-clients).

Заменяет блок b-aux-actions

##API:##
Принимает аргументы:
- groups: {
    title: 'Группа ссылок',
    links: [
        {
            url: 'url',
            title: 'Ссылка'
        },
        {
            block: 'myblock'
        },
        {
            [
                {
                    block: 'block1',
                },
                {
                    block: 'block2',
                }
            ]
        }
    ]
}
- chief: { //Главный представитель
    name: 'ФИО',
    email: 'example@example.com'
}
- manager: { //Менеджер
   name: 'ФИО',
   email: 'manager@example.com'
}
-footnotes: [ //Подписи
    {
        footnoteNo: '1',
        text: 'Подпись 1'
    },
    {
        footnoteNo: '2',
        text: 'Подпись 2'
    }
]
-inThreeColumns: true // нужно ли разбивать в колонки ПО ТРИ элемента
-hasServiceLink: true // флаг, что есть ссылка на кампании в директе/баяне - она не должна уезжать одна во вторую колонку
// бывает в баяне

##Примеры:##
p-campaigns__aux-actions.bemtree.xjst
p-clients__aux-actions.bemtree.xjst
p-manager-my-clients__aux-actions.bemtree.xjst

##Мейнтейнеры:##
[anyakey](https://staff.yandex-team.ru/anyakey)
