Данный блок позволяет отобразить блок b-media-topics в виде попапа.
В качестве параметров можно задать хэш options, который будет передаваться в моду js блока b-media-topics. Описание свойств этого хэша смотрите в описании блока b-media-topics.

Преобразует входной bemjson вида:

    {
        block: 'b-media-topics-popup',
        options: {/* параметры */}
    }

в следующий bemjson:

    {
        block: 'b-popupa',
        mods: {theme: 'ffffff', 'has-close': 'yes', direction: 'down', adjustable: 'no'},
        content: [
            {elem: 'tail'},
            {elem: 'close'},
            {
                elem: 'content',
                content: {
                    block: 'b-media-topics-popup',
                    content: {
                        block: 'b-media-topics',
                        js: {/* параметры */}
                    }
                }
            }
        ]
    }
