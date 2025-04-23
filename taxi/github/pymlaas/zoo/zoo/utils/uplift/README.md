# Uplift

Привет, товарищ

Перед тобой лучшая в мире библиотека по оценке эффектов воздействия (Treatment Effects). Инструмент активно развивается. Извини, если где-то не поддержится обратная совместимость. Здесь будет неполная документация по более менее стабильным фичам.

Все картинки документации можно вопрозвести кодом из docs.

## Зачем мне это?

Задачка

цитаты, мысли
про регуляризацию и далее

мысль -- при ранжировании нам плевать на bias. Нам важен порядок. А если делим?

examples and datasets



Задачка

Пока что мы забудем про то, что разные водители стоят сервису по разному (расслабьте булки, это всего-лишь деньги. Что не сделаешь для всемирного счастья)

## Что такое Treatment Effect

Теория
...
...
...
...



Код


```Python
from zoo.utils.uplift.hte import HeterogenousTreatmentEffects
from catboost import CatBoostRegressor

main_model = HeterogenousTreatmentEffects(CatBoostRegressor(l2_leaf_reg=0.5))
main_model.fit(X_train, y_train, t_train)
prediction = main_model.predict(X_test)
```

картинка

## Propensity score (Только финальную версию тоже)

Теория
А что если мы имеем дело с несколькими эксперментами

В чем проблема (спойлер)

А еще же бывает такое, что nonexperimental data

Да, 2 модели

Как не вполне правильно
```Python
... ... ...
```

Интуиция

double robustness +++

Код

```Python
from zoo.utils.uplift.propensity_score import PropensityScore
from catboost import CatBoostClassifier

propscore_model = PropensityScore(CatBoostClassifier(iterations=10, l2_leaf_reg=10, cat_features=[2, 19]))
propscore_model.fit(X_train, t_train)
propscore_predictions = model.resample(X_test)

sample_weight = propscore_predictions['sample_weight']

# картинку

main_model.fit(X_train, y_train, t_train, sample_weight=sample_weight)

prediction = main_model.predict(X_test)
```

Парни! Слишком много кода. Как бы автоматом перенаправлять sample_weight и обучать 2 модели сразу одной строчкой?
```Python
from zoo.utils.uplift.resampling import ResamplingPipeline

final_model = ResamplingPipeline(steps=[
  ('propscore', propscore_model),
  ('main', main_model)
)
final_model.fit(X=X_train, y=y_train, t=t_train) # Сорян! Positional arguments тут пока не работают
prediction = final_model.predict(X_test)
```

Окей, но что это означает теперь, что я не могу для обучения разных моделей использовать разные датасеты?

```Python
final_model.fit(X=X_train, y=y_train, t=t_train, propscore_X=X_train[0,1])
prediction = final_model.predict(X_test)
```

Никто не заставляет тебя использовать CatBoost, если ты его не любишь

```Python
from xgb import XGBRegressor
from sklearn.preprocessing import OneHotEncoder
frim sklearn.linear_model import LogisticRegression

doglover_main_model = HeterogenousTreatmentEffects(XGBRegressor(reg_lambda=0.5))
doglover_propscore_model = PropensityScore(make_pipeline(OneHotEncoder, LogisticRegression))

doglover_final_model = ResamplingPipeline(steps=[
  ('propscore', doglover_propscore_model),
  ('main', doglover_main_model)
)
doglover_final_model.fit(X=X_train, y=y_train, t=t_train, propscore__X=X_train[0,1])
prediction = doglover_final_model.predict(X_test)
```

## LOOP Estimator
TBD

## ParetoBorder
Вспомним про деньги. Деньги это не последнее. Я сэкономлю денег, чтобы на оставшиеся сделать мир еше лучше

## Оценка качества

https://web.stanford.edu/~jgrimmer/het.pdf

Код
```Python
from zoo.utils.uplift.evaluation import efficiency_curve

y, threshold = efficiency_curve([m_test, y_test], t_test, -prediction)

plt.plot([y[0, 0], y[-1, 0]], [y[0, 1], y[-1, 1]], 'k--')
plt.plot(y[:, 0], y[:, 1], 'b')
plt.xlabel(u'Траты на водителя')
plt.ylabel(u'Доп заказов на водителя')
plt.show()
```


## Полезности

Не знаю как вы, а я храню данные в json/yson или сsv ну и точно не в numpy array. Как бы этот зоопарк подружить с моими данными? -- не оч понятно

```Python
from zoo.utils.uplift.dict_extractor import DictExtractor

extractor = DictExtractor( #need fallbacks!!! smart, so that still falls if. MB ONLY X???
    {
        't':'treatment',
        'y': 'target_n_orders_7',
        'propscore__X': ['task'],
        'X': features
    },
    ret_args=['X']
)

final_model = ResamplingPipeline(steps=[
  ('extractor', extractor)
  ('propscore', propscore_model),
  ('main', main_model)
)

final_model.fit(train_data)
final_model.predict(test_data)
```

Так, например, модель можно применить с помощью nile_predict

```Python
from zoo.utils.nile_helpers.mappers import nile_predict
nile.stream_with_data.nile_predict(final_model)
```


## Литература
https://www.nber.org/papers/w22627 Regression Discontinuity и оценка спроса на примере Uber
Более модные методы regression discontinuity
IV estimation -- помоднее статью

Heterogenous Treatment Effects: https://web.stanford.edu/~jgrimmer/het.pdf
Policy Learning: так на самом деле назвается модель оптимального оффера: https://arxiv.org/abs/1702.02896 здесь про то, что делать, если тебе не разрешают использовать какие-то фичи, но очень хочется. https://arxiv.org/abs/1810.04778 здесь про то, как выбирать из нескольких альтернатив, а не из двух
https://arxiv.org/abs/1708.01229 LOOP estimator -- как в стат тесте скушать часть дисперсии за счет фичей
Престратификация
Обзорную статью про observational studies (controlling and propensity score)
Вот так можно изучать эффект на годовой LTV, если у нас нет роскоши ждать после эксперимента год, чтобы его пронаблюдать https://arxiv.org/pdf/1603.09326 Если коротко -- надо иметь прогнозную модель LTV по одной неделе, и смотреть эффект на прогноз. В статье описывается, что нужно предположить о мире, чтобы уверовать в этот метод.
