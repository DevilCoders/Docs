===b-model===
наследник блока i-model, у которого определена схема данных (шаблон) и уникальное имя

всё начинается с метода %%register%%
%%(javascript)
    BEM.blocks['b-model'].register(<<имя модели>>, { <<схема данных модели (шаблон)>> });
%%

====Шаблон модели====
%%(javascript)
{
    fields: {
        //...
    },
    
    validateRules: {
        //<<для каждого поля нуждающегося в валидации описываем правила проверки>>
    }
}
%%

Шаблон однозначно определяется именем модели
%%(javascript)
    BEM.blocks['b-model'].register('b-time-targeting', {
        fields: {
            timeTarget: {type: 'string', input: 1, fromServer: 1, toServer: 1},
            timeTargetMode: {type: 'string', fromServer: 1, toServer: 1, 'default': 'simple'},
            timeTargetSelectedCoef: {type: 'number', input: 1, 'default': 100, precision: 0},
            counter: {type: 'number'}
        },

        validateRules: {
            'counter': {
                list: [

                        {
                            name: 'min',
                            id: 'min',
                            warning: 1, // если warning не указан -- это ошибка
                            value: 40,
                            text: iget('Кампания должна быть включена не менее 40 часов в рабочие дни')
                        }

                ],
                condition: function() {
                    // this - конкретный инстанс модели b-time-targeting, который инициировал метод validate
                }

            }
        }
    });
%%
