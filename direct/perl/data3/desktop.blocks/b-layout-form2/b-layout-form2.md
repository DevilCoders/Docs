#b-layout-form2#
Будущий универсальный грид.

Сейчас принимает:
а) массив groups следующего вида:
-groups:
    --name(optional) - имя группы
    --mixes - миксы для группы
    --cells - массив ячеек
        --left: - элемент для левой колонки
            --mixes: - миксы для левой колонки
        --center: - для центральной
            --mixes: - миксы для центральной колонки
        --right: - для правой
            --mixes: - миксы для правой колонки

-header: заголовок блока, ставится над группами
-submit: элемент для футера (сейчас там всегда кнопка submit)
    --position: в какую колонку положить элемент
    --control: сам контрол
-hiddenInpurs: массив скрытых элементов

##Пример##
Используется в b-campaign-settings

{
    block: 'b-layout-form2',
    hiddenInputs: [
      { name: 'fio', value: campaign.fio },
      { name: 'cmd', value: data.new_camp == 1 ? 'saveNewCamp' : 'saveCamp' }
    ]
    //формат как у групп
    header: { name: '', cells: []}
    submit: {
        position: 'left',
        //любой элемент
        control: applyCtx({ block: 'b-campaign-settings', mods: { type: 'mobile-content' }, elem: 'submit' })
    },
    groups: applyCtx([
        {
            mixes: [{ block: 'b-campaign-settings', elem: 'campaign-name-group' }],
            cells: [
                data.currentAgency && applyCtx({
                    block: 'b-campaign-settings',
                    elem: 'campaign-agency'
                }),
                applyCtx({
                    left: {
                        block: 'b-campaign-settings',
                        elem: 'label',
                        text: iget('SMS-уведомления'),
                        help: {
                            url: u.getHelpUrl('sms-alerts'),
                            width: 1100
                        }
                    },
                    right: applyCtx({
                        block: 'b-campaign-settings',
                        elem: 'sms-warnings',
                        campaign: this.data.campaign
                    })
                })
            ]
        },
        {
            mixes: [{ block: 'b-campaign-settings', elem: 'campaign-settings-geo' }],
            name: iget('География'),
            cells: [
                applyCtx({
                    block: 'b-campaign-settings',
                    elem: 'campaign-geo'
                }),
                applyCtx({
                    block: 'b-campaign-settings',
                    elem: 'campaign-extended-geotargeting'
                })
            ]
        },
    ])
}

###Мейнтейнеры###
@anyakey[https://staff.yandex-team.ru/anyakey]
