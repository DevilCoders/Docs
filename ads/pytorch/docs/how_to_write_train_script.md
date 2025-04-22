<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Как работает обучение.](#%D0%BA%D0%B0%D0%BA-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D1%82-%D0%BE%D0%B1%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5)
- [Интеграция моделей в пайплайны ads_pytorch](#%D0%B8%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D0%B5%D0%B9-%D0%B2-%D0%BF%D0%B0%D0%B9%D0%BF%D0%BB%D0%B0%D0%B9%D0%BD%D1%8B-ads_pytorch)
  - [Loss](#loss)
  - [wrap_model_with_concat_wrapper](#wrap_model_with_concat_wrapper)
    - [Как правильно расфасовать параметры по буферам](#%D0%BA%D0%B0%D0%BA-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D1%8C%D0%BD%D0%BE-%D1%80%D0%B0%D1%81%D1%84%D0%B0%D1%81%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D0%BF%D0%BE-%D0%B1%D1%83%D1%84%D0%B5%D1%80%D0%B0%D0%BC)
    - [Как разделить параметры в разные буферы](#%D0%BA%D0%B0%D0%BA-%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB%D0%B8%D1%82%D1%8C-%D0%BF%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B-%D0%B2-%D1%80%D0%B0%D0%B7%D0%BD%D1%8B%D0%B5-%D0%B1%D1%83%D1%84%D0%B5%D1%80%D1%8B)
- [Итого](#%D0%B8%D1%82%D0%BE%D0%B3%D0%BE)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

**ВАЖНО:** предполагается, что вы уже прочитали tutorial по тому, как строить модельки.

{{toc}}

# Как работает обучение.
Библиотека ads_pytorch сейчас поддерживает однохостовое асинхронное data-parallel multi-gpu обучение с автоматическим распараллеливанием. Это значит, что вы просто отдаете модель обучалке и она сама настраивает распараллеливание обучения по CPU/GPU на хосте.

# Интеграция моделей в пайплайны ads_pytorch
Чтобы запускать скрипт в любом пайплайне обучения ads_pytorch, нужно его специальным образом оформить. Для этого в скрипте должен быть наследник класса [ModelFactory](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/nirvana/model_factory.py?rev=r7777100#L44) ( [пример](https://a.yandex-team.ru/arc/trunk/arcadia/junk/alxmopo3ov/ad_transformer_v2/multiseq_v2/script.py?rev=r7960778#L151) ).

Как и раньше, проще рассмотреть end-to-end пример целой фабрики

```(python)
class SimpleDSSM(IDeployableModel):
    def __init__(
        self,
        user: torch.nn.Module,
        banner: torch.nn.Module,
        embeddings: BaseEmbeddingModel
    ):
        super(SimpleDSSM, self).__init__(embedding_model=embeddings)
        self.user = user
        self.banner = banner
        self.top_level = TzarDoubleTopLevelModel()

    def deployable_model_forward(self, embedded_inputs: List[torch.Tensor]) -> Any:
        user = self.user(embedded_inputs)
        banner = self.banner(embedded_inputs)
        return self.top_level(user, banner)


# Запускалка скриптов сама найдет наследника фабрики в скрипте
class TrainDescription(ModelFactory):
    # Мы запрещаем делать кастомные __init__ в фабриках, чтобы при расширении функционала и добавлении новых полей сохранять обратную совместимость
    # Этот метод вызывается в конце конструктора фабрики и там всегда есть все-все-все поля
    # Сейчас нас интересует поле model_config_path - это путь к файлу с конфигом модели. Мы его сразу распарсим
    def __model_factory_post_init__(self):
        with open(self.model_config_path, 'rt') as f:
            self.parsed_model_conf = json.load(f)

    def create_model(self) -> IDeployableModel:
        # Тут для вас не должно быть ничего нового, если вы читали tutorial по конструированию модельки
        embedding_model = build_embedding_model(features_config=self.parsed_model_conf["model"]["features"])
        user_model = build_network(
            cfg=self.parsed_model_conf["model"]["user"],
            embedding_descriptors=embedding_model.embedding_descriptors,
            feature_order_holder=embedding_model.get_feature_order_holder()
        ).net
        banner_model = build_network(
            cfg=self.parsed_model_conf["model"]["banner"],
            embedding_descriptors=embedding_model.embedding_descriptors,
            feature_order_holder=embedding_model.get_feature_order_holder()
        ).net
        model = SimpleDSSM(user=user_model, banner=banner_model, embeddings=embedding_model)
        # Одна из важнейших оптимизаций производительности. К сожалению, ее практически невозможно унести под капот от пользователя,
        # так что нужно научиться ей пользоваться
        return wrap_model_with_concat_wrapper(model)

    def create_optimizer(self, model) -> ParameterServerOptimizer:
        model_conf = self.parsed_model_conf["model"]

        optimizers = [
            SharedAdam(
                # Когда вы используете concat_wrapper (а вы ВСЕГДА должны его использовать), нужно засовывать в оптимайзер сконкатенированные параметры
                # у обертки появляется метод buffer_parameters() - итератор по сконкатенированным буферам глубоких параметров модели
                # Если вы НЕ используете concat_wrapper у IDeployableModel, то вам нужно дернуть метод deep_parameters()
                model.buffer_parameters(),
                lr=model_conf["nn"]["learning_rate"],
                amsgrad=True
            )
        ]

        # Для создания оптимайзеров над эмбеддингами для BaseEmbeddingModel есть автоматизация
        optimizers += build_embedding_optimizers(
            embedding_model=model.net.embedding_model,
            features_config=model_conf["features"]
        )

        # Метод create_loss всегда должен возвращать ParameterServerOptimizer. Вообще это легаси, так как
        # он под капотом все равно раздербанивается на отдельные оптимизаторы, но он все еще является удобной оберткой
        # для обычных последовательных запусков обучения
        return ParameterServerOptimizer(*optimizers)

    def create_loss(self) -> torch.nn.modules.loss._Loss:
        return torch.nn.BCEWithLogitsLoss(reduction="mean")

    # Специальный метод, чтобы на основании описания модели подать в пайплайн список фичей и не дублировать его в пайплайно-специфичных
    # секциях, отвечающих за загрузку данных
    def get_required_features_list(self) -> Optional[List[str]]:
        feature_cfg = self.parsed_model_conf["model"]["features"]
        descrs = read_embedding_descriptors(config=feature_cfg["embeddings"])
        embedding_features = sum([[x.string_name for x in descr.features] for descr in descrs], [])
        external_features = feature_cfg.get("external", [])
        return embedding_features + external_features

```

Технически, пайплайны ads_pytorch сами найдут в вашем скрипте наследника ModelFactory:
1. Находим все классы-наследники ModelFactory в неймспейсе вашего скрипта
2. Проверяем, что они образуют непрерывную цепочку наследования. Если где-то есть вилка - автоматика падает и говорит, что не может однозначно определить фабрику
3. Если цепочка одна, берем последнего наследника

Если же вам почему-то нужно импортировать несколько фабрик, то можно явным образом прописать, какую фабрику брать из скрипта, минуя автоматику, с помощью глобальной переменной

```(python)
__ADS_PYTORCH_CURRENT_MODEL_FACTORY_CLS__ = MyModelFactory
```

## Loss
```create_loss``` должен возвращать torch.nn.Module с методом forward такого формата:
```(python)
class MyLoss(torch.nn.Module):
    def forward(predictions, targets):
        pass
```
* predictions - то, что вернула ваша IDeployableModel из forward-pass
* targets - либо один тензор, либо словарь ```str->torch.Tensor```. Один тензор сделан для консистентности с большинством простых pytorch loss. Если в конфиге обучения будет описан один таргет, то приедет тензор, в противном случае - словарь.

## wrap_model_with_concat_wrapper
Оптимизация производительности для апдейтов мелких параметров. Развесистые модели с кучей подсетей часто содержат в себе множество небольших параметров, которые скапливаются в довольно значительный объем разрозненных мелких тензоров. Оптимайзеры торча работают так: [проходятся по всем параметрам модели](https://github.com/pytorch/pytorch/blob/master/torch/optim/adam.py#L77) в цикле и апдейтят их. Апдейты шедулятся в один и тот же CUDA stream и выполняются строго последовательно вне зависимости от размера тензора. Для большинства моделей это выливается в python цикл for по 1000+ параметрам, каждый параметр запускает еще пачку последовательных операций вида "сложи 10 флотов". Получается абсолютно неоптимальное распределение нагрузки на видеокарту. Учитывая особенности обучения, такой оптимайзер резко становится bottleneck'ом.

wrap_model_with_concat_wrapper - способ автоматического решения этой проблемы. Поскольку примерно все методы стохастической оптимизации покоординатные, то можно объединять мелкие параметры в один здоровый во время апдейтов. wrap_model_with_concat_wrapper проходится по параметрам модели и собирает их в буферы. Во время апдейтов, апдейты работают поверх буферов. Буферов обычно не более 10 в модели, что позволяет засылать на видеокарту апдейты по большим тензорам и на порядок эффективнее утилизировать GPU.

Чтобы заиспользовать, надо сделать вот так
```(python)
model: DSSM
model = wrap_model_with_concat_wrapper(model)

# Вот так можно достать обернутую сеть
net: DSSM = model.net

# Вот так нужно подавать в оптимайзеры сконкатенированные параметры
optim = torch.optim.Adam(model.buffer_parameters())
```

Почему реализован именно так, почему бы автоматически не конкатенировать параметры/стейты оптимайзера во время апдейтов?
Короткий ответ такой:
1. В большинстве оптимизаторов есть тензоры, которые не совпадают по размеру с параметрами и их автоматическая конкатенация ни к чему хорошему не приведет. Автоматические попытки угадать "а как же работает код пользователя" обычно проваливаются
2. Более абстрактно, в оптимайзере может быть написан произвольный код по обработке этих параметров, который может поломаться

Если же сразу подать буфер в оптимайзер, то не будем ничего угадывать: код оптимайзера сам создаст корректное состояние конкретно для этого буфера и все будет работать.

### Как правильно расфасовать параметры по буферам
Во-первых, очевидно, что параметры, которые едут в разные оптимайзеры или имеют разные гиперпараметры внутри одного оптимайзера, должны быть в разных буферах. Во-вторых, чуть менее очевидно, параметры должны быть нарезаны по буферам так, что **либо есть градиенты по всем параметрам в буфере, либо нет ни по одному**.

Допустим, у нас есть непрерывный буфер, и в модели рандомно были отключены некоторые параметры на текущем forward-backward. Какие есть варианты развития?
1. Занулить градиенты для этих параметров
2. Попробовать правильно нарезать стейт и отрубить эти параметры

Первый вариант плох тем, что на самом деле нулевой градиент означает, что **параметр уже в критической точке**. Такое зануление на самом деле может убивать стейт оптимайзера и мешать обучению.

Второй вариант плох тем, что нам придется делать какую-то автоматическую разрезалку параметр

### Как разделить параметры в разные буферы
Для разделение параметров есть методы get_mark, mark_tensor, mark_module.

# Итого
Итого сейчас есть:
1. Моделька
2. Правильно написанный скрипт запуска
3. Правильно составленный конфиг **самой модельки**

Осталось два шага: разобраться в пайплайнах запуска и специфичных для них настройках и оставить единый конфиг модели + пайплайна
