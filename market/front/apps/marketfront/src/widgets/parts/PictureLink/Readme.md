##PictureLink

Виджет для показа не кликабельной/кликабельной картинки.
Работет только с сущьностью типа `formula`.

### Пример минимально необходимой декларации

```javascript
const decl = {
    entity: "widget",
    name: "PictureLink",
    id: 37611130,
    loadMode: "default",
    resources: {
        garsons: [
            {
                id: "CustomFormulas",
                params: {
                    data: [
                        {
                            entity: "formula",
                            id: 37611133,
                            pictures: [
                                {
                                    entity: "picture",
                                    width: "732",
                                    height: "1200",
                                    url: "//avatars.mdst.yandex.net/get-marketcms/69555/img-ff75ba24-3e14-4331-9bfe-5d879a7d3ca2.png/optimize",
                                    thumbnails: [
                                        {
                                            entity: "thumbnail",
                                            id: "366x3000",
                                            containerWidth: "366",
                                            containerHeight: "3000",
                                            width: "366",
                                            height: "600",
                                            densities: [
                                                {
                                                    entity: "density",
                                                    id: "1",
                                                    url: "//avatars.mdst.yandex.net/get-marketcms/69442/img-17983e28-8eac-450b-b314-14ec4d7538fe.png/optimize"
                                                },
                                                {
                                                    entity: "density",
                                                    id: "2",
                                                    url: "//avatars.mdst.yandex.net/get-marketcms/69442/img-2d0acd8e-fa73-4bed-bb19-d47489e2142f.png/optimize"
                                                }
                                            ]
                                        },
                                    ]
                                }
                            ]
                        }
                    ]
                }
            }
        ]
    },
    props: {
        subtitle: {
            type: "default"
        },
        titleParams: {
            size: "m",
            type: "default"
        },
        paddingTop: "normal",
        paddingBottom: "normal",
        paddingLeft: "normal",
        paddingRight: "normal",
        theme: "default",
        titleStyle: "default",
        compensateSideMargin: false,
        layout: "auto"
    }
}
```

### Как работает

Выбирает первую картинку из полученного списка и отдает на отрисовку контейнеру `Formula`
