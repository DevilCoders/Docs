r109458
## b-group-tags2-controller ##
Блок, реализующий редактирование тегов в группе
Намешивается на b-group-tags2
Предполагается, что для реализации поведения отличного от базавого должны быть реализованы модификаторы блока, где будут переопределены `_onEdit` и `_onSave`

## Автор ##
[alkaline](https://staff.yandex-team.ru/alkaline)

## Пример ##
    {
        block: 'b-group-tags2',
        mix: {
            block: 'b-group-tags2-controller',
            js: {
                modelParams: {
                    group: {
                        name: this.groupModelName,
                        id: this.groupId
                    },
                    campaign: {
                        name: 'm-campaign',
                        id: this.data.campaign.cid
                    }
                }
            }
        },
        tags: this.ctx.tags
    }
