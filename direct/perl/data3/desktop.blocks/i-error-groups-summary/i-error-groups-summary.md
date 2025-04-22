#i-error-groups-summary#

##Описание##
Блок конвертации данных о валидации в данные для отображения в b-error-groups-summary

###Автор###
[alkaline](https://staff.yandex-team.ru/alkaline)

##Пример##

```
    //request - запрос на сохранение групп, groupsModels - массив моделей групп
    request.get(params, function(data) {
        if (data.errors) {
            var groupData = groupsModels.map(function(groupModel) {
                    return BEM.blocks['i-error-groups-summary'].groupToSummaryData(groupModel.toJSON());
                }),
                errorsSummary = BEM.blocks['i-error-groups-summary'].summarizeErrors(groupData, data.errors);

            //...
        }
    })
```
