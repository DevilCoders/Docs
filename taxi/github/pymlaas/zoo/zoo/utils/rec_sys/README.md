##О чём здесь написано
Этот файл призван рассказать как всё устроено в пакете и почему именно так 

## Собственно, контент

#### Как выглядит pipeline рекомендательной системы в этом пакете:
1. Подготовка данных (нужно создать таблицу с запросом (request) и релевантными таргетами (targets))
2. Получение для каждой записи списка кандидатов с релевантностью каждого кандидата
3. Деление таблицы на трейн и тест  
4. Подготовка таблиц к обучению (сэмлирование + простановка весов)
5. Извлечение признаков на трейне, и тесте (здесь тест это для автостопа)
6. Обучение модели на трейне с eval-ом на тесте
7. Применение модели на тесте
8. Оценка метрик на тесте


#### Как предлагается реализовывать этот pipeline

**Концепция factory_object**

Некоторые объекты очень плохо сериализуются, поэтому их нужно создавать внутри map или reduce. Пока мы полностью не решили эту проблему, поэтому будем пользоваться этой концепцией. Она сотостоит в том, чтобы вместо объекта принимать функцию, которая при вызове этот объект создаёт. Тогда мы сможем создавать несериализуемые объекты прямо на кластере. В светлом будущем мы с этим поборемся и перепишем пайплайн на project-ы.

**1. Подготовка данных**

Рекомендуется писать функцию collect каждый раз заново для каждого эксперимента, но общую функциональность при сборе данных выделять в отдельные переиспользуемые модули

**2. Получение кандидатов**

Есть какие-то стандартные селекторы или релевансеры, но по аналогии с предыдущим пунктом в каждой задаче он будет свой

Однако, стоит придерживаться следующего интерфейса:
```
class CandidatesExtractor:
    def __call__(self, request):
        # do some stuff
        return candidates
```

```
class TargetExtractor:
    def __call__(self, record):
        # do some stuff
        return list_of_relevances_of_objects
```

Почему `CandidatesExtractor.__call__` принимает только `request`, а `TargetExtractor.__call__` принимает весь `record`? Потому что `CandidatesExtractor` – это класс, который потенциально будет применяться в продакшне, поэтому у него не должно быть никаких дополнительных зависимостей. А `TargetExtractor` нужен только для аналитики, поэтому для гибкости может зависеть от чего угодно. 


**3. Деление таблицы на трейн и тест** 

Надо написать splitter для одного record. 

    
```
class Splitter:
    def __call__(self, record):
        return True/False/None
        # None значит вообще не участвует в обучении
        # 'train' – train
        # 'test' – test
```


**4. Подготовка таблиц к обучению (сэмлирование)**

Надо писать sampler от одного record.

```
class Sampler:
    def __call__(self, record):
        # do some stuff
        return list_of_indices_of_candidates, weights_of_dataset_indexed_candidates
        # может вернуть пустой список или None, если хочется заигнорировать объект
```

Объект будет использоваться функцией  `pipeline.extend_by_dataset_indices`


**5. Извлечение признаков**

Нужно написать свой надо только extractor

```
class FeaturesExtractor
    def __call__(self, request, candidates, indices=None):
        all_candidates = np.array(candidates)
        if indices is not None:
            candidates = all_candidates[indices]

        # do some stuff for objects using request and all_candidates
        return features_of_candidates_by_indices
```

**6. Обучение модели**
Обучать надо на Нирване

**7. Применение модели на тесте**
Нужно написать свой rec_model

```
class RecModel:
    def __call__(self, request):
        candidates = CandidatesExtractor.__call__(request)
        features = FeaturesExtractor.__call__(request, candidates)
        relevance = mxnet.__call__(features)
        return objects
```


### Как удобно всё реализовать
Для работы предлагается каждый раз реализовывать класс `factory.BaseRecFactory`,
в которой создаются все необходимые объекты.

Клиентом `factory` является `ExperimentManager`, который умеет, используя фабрику,
совершать все выше описанные шаги и предоставляет интерфейс для настройки
эксперимента. 

Базовый интерфейс под обучение на nile написан в модуле `pipelines.nile.exp_manager`
