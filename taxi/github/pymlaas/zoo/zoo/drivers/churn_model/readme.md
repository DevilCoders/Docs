timemachine.py
- OrdersTimeMachine
- RangeTimepoints
- DefaultTimepoints



проверить, что с и без другим источников, фичи по водителям считаются праивльно/одинаково

    # ?? непонятно, тут надо сегдняшнюю дату или сегодняшнюю минус 50 дней

    # здесь создам для всего рейнджа дат. а потом буду в зависимости от дней отсутствия
    # фильтровать срезы

    # генерятся даты от первого появления водителя до того времени, как фичи заказнчиваются
    
data_context.py

targets.py
- DriverTarget

features_extractor.py
- FeaturesExtractor
 # переписать
 
 
 apply_model.py
 (строит фичи)
 
 folder: churn_model
 
 targets.py
 
 train_model.py

    # срезы продумать - куда их класть, где подсчитывать (очевидно, в фичах)
    # посмотреть, что за self.offset (утечка в таргет? аккуратно)
    # TODO когда обучать модель - обучать на тех, кто отсутствовал 7 дней - вернется или нет

    # TODO: научиться из максимального окна получать остальные
    # TODO: переписать features_extractor
    # 
    # windowsextractor - из максимлаьного окна получает мЕньшие
    # statsextractor - принимает records (и потом к каждой record применятся features extractor)
    # featuresextractor - принимает именно record
    # arithmetic_class - для всякой фигни с числовыми фичами
    # cat features
    # munerical features