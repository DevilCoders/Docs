<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Что такое ads_pytorch и кому она нужна](#%D1%87%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-ads_pytorch-%D0%B8-%D0%BA%D0%BE%D0%BC%D1%83-%D0%BE%D0%BD%D0%B0-%D0%BD%D1%83%D0%B6%D0%BD%D0%B0)
- [Работа с эмбеддингами](#%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%8D%D0%BC%D0%B1%D0%B5%D0%B4%D0%B4%D0%B8%D0%BD%D0%B3%D0%B0%D0%BC%D0%B8)
  - [HashEmbedding](#hashembedding)
    - [Формат входных данных](#%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82-%D0%B2%D1%85%D0%BE%D0%B4%D0%BD%D1%8B%D1%85-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85)
    - [compute_mode](#compute_mode)
    - [Последовательности эмбеддингов](#%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D1%8D%D0%BC%D0%B1%D0%B5%D0%B4%D0%B4%D0%B8%D0%BD%D0%B3%D0%BE%D0%B2)
    - [Обобщенный код любых вычислений внутри HashEmbedding](#%D0%BE%D0%B1%D0%BE%D0%B1%D1%89%D0%B5%D0%BD%D0%BD%D1%8B%D0%B9-%D0%BA%D0%BE%D0%B4-%D0%BB%D1%8E%D0%B1%D1%8B%D1%85-%D0%B2%D1%8B%D1%87%D0%B8%D1%81%D0%BB%D0%B5%D0%BD%D0%B8%D0%B9-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B8-hashembedding)
  - [BaseEmbeddingModel и IDeployableModel](#baseembeddingmodel-%D0%B8-ideployablemodel)
- [Фабрики моделей](#%D1%84%D0%B0%D0%B1%D1%80%D0%B8%D0%BA%D0%B8-%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D0%B5%D0%B9)
  - [BaseEmbeddingModel json](#baseembeddingmodel-json)
  - [SubNetworks](#subnetworks)
    - [Рекурсивное пострение глубоких архитектур](#%D1%80%D0%B5%D0%BA%D1%83%D1%80%D1%81%D0%B8%D0%B2%D0%BD%D0%BE%D0%B5-%D0%BF%D0%BE%D1%81%D1%82%D1%80%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B3%D0%BB%D1%83%D0%B1%D0%BE%D0%BA%D0%B8%D1%85-%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80)
    - [Конфигурирование фабрик архитектур. Библиотека архитектур](#%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D1%84%D0%B0%D0%B1%D1%80%D0%B8%D0%BA-%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80-%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA%D0%B0-%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80)
    - [Библиотечные слои](#%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D1%87%D0%BD%D1%8B%D0%B5-%D1%81%D0%BB%D0%BE%D0%B8)
      - [GenericFeedForwardWithNormalizers](#genericfeedforwardwithnormalizers)
      - [GenericFeedForwardWithHeads](#genericfeedforwardwithheads)
      - [MultisequenceTransformerEncoder2](#multisequencetransformerencoder2)
        - [key_mask](#key_mask)
        - [Встроенные типы TransformerEncoder](#%D0%B2%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-%D1%82%D0%B8%D0%BF%D1%8B-transformerencoder)
          - [torch](#torch)
          - [ads_pytorch](#ads_pytorch)
          - [Рекомендуемый TransformerEncoder](#%D1%80%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D1%83%D0%B5%D0%BC%D1%8B%D0%B9-transformerencoder)
        - [Встроенные типы построений последовательностей в multisequence_tranformer_input_sequence_builder](#%D0%B2%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-%D1%82%D0%B8%D0%BF%D1%8B-%D0%BF%D0%BE%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BD%D0%B8%D0%B9-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B5%D0%B9-%D0%B2-multisequence_tranformer_input_sequence_builder)
          - [plain_sum](#plain_sum)
          - ["densenet"](#densenet)
          - [Рекомендуемые настройки](#%D1%80%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D1%83%D0%B5%D0%BC%D1%8B%D0%B5-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B8)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

**ВАЖНО:** данный tutorial предполагает, что вы уже знаете, что такое нейронные сети, имеете базовое представление о наиболее распространенных архитектурах и наиболее успешных приложениях нейросетей, знакомы с фреймворком PyTorch, знакомы с азами машинного обучения.

{{toc}}

# Что такое ads_pytorch и кому она нужна

ads_pytorch - библиотека-надстройка над PyTorch для обучения нейронных сетей. Основной прицел - **рекомендательные системы и табличные данные**. В целом, никаких ограничений на классы моделей нет, можно учить и CV, и BERT, и т.д., но примерно все оптимизации и фишечки библиотеки направлены именно на табличные данные.

Под табличными данными мы понимаем слабо структурированные неоднородные данные и не накладываем никаких ограничений на то, как описывается объект обучающей выборки. Там могут быть произвольные множества чего-то, тексты, списки айдишников, или даже множества структурированных объектов.

Примеры (по возрастанию сложности):
1. Айдишник товара, айдишник пользователя, айдишник производителя товаров (one-hot категориальные фичи)
2. Дата добавления товара, цена товара, расстояние пользователя до магазина (float фича)
3. Текстовое описание товара (multi-value категориальная фича)
4. Картинка товара (float матрица)
5. Счетчик топ категорий товаров, которые просматривает пользователь - множество айдишников категорий, и для каждого айдишника есть еще float счетчики вида "как давно в последний раз смотрел, сколько всего раз смотрел и т.д." (множество categorical ключей + float массив для каждого ключа)
6. Последние N запросов пользователя в поиске по товарам - множество текстов и timestamp'ов запросов
7. to be continued...

В больших рекомендательных системах, как правило, есть все эти типы данных и множество других. Сейчас в мире господствует концепция **end-to-end обучения**: засунуть как можно более сырые данные разом в одну модель и предоставить модели самой выучивать внутренние представления этих данных. ads_pytorch - это, прежде всего, инструмент для удобного описания и быстрого обучения моделей над максимально разнородными табличными данными больших объемов.

В течение tutorial мы будем проходиться по основным возможностям библиотеки и попутно решать поставленную задачу. Договоримся сразу о верхнеуровневой архитектуре: это будет DSSM-like модель, для товара и для пользователя будет своя нейросеть, каждая нейросеть выдает вектор. Предсказанием будет скалярное произведение векторов пользователя и товара `𝛼 * u^Ti + b`, где:
* u - вектор пользователя (user)
* i - вектор товара (item)
* b - константа сдвига (он же bias)
* 𝛼 - мультипликатор при скалярном произведении, число

# Работа с эмбеддингами
Работа с любыми категориальными фичами из коробки - это, наверное, главное преимущество нейросетевого подхода над всеми остальными классами моделей машинного в рекомендательных системах, в т.ч. над градиентным бустингом. CatBoost пытался решить эту проблему, однако категориальные фичи больших размерностей (скажем, 30-40 миллионов уникальных ключей) там работают плохо. Табличные данные как раз славятся наличием большого количества разнородных категориальных фичей, и мы сделали собственные наработки.

Традиционный подход к эмбеддингам в нейронных сетях примерно следующий:
1. **Варим словарь**: проходимся по датасету, собираем множество фичей и их встречаемость, удаляем часть ключей и т.д., оставляем N фичей в словаре. Иногда в этот же пункт входит превращение строк текста в набор ключей, но мы будем считать, что это отдельная операция, напрямую не связанная с нейросетью, и все кат фичи/тексты у нас - ключи.
2. Нумеруем ключи наших фичей от 0 до N-1
3. Создаем плотный двумерный массив размера N x D, где D - размер эмбеддинга, фиксируем набор ключей в словаре
4. Фиксируем набор ключей в словаре, дообучаем для них веса. **Нет операций вставки или удаления ключа**

Такой подход неплохо работает для более-менее статичных NLP задач, где есть единственная категориальная фича - текст с BPE словарем, рассчитанный заранее по огромному датасету. Однако для рекомендательных систем характерно огромное количество динамически меняющихся категориальных фичей. Например, в текущей рекламной модели уже 130 категориальных фич (TODO ссылка). В таком сеттинге подход начинает трещать по всем фронтам:
* **Дообучение моделей**. В рекомендательных системах модели обычно дообучаются на свежих данных под свежие интересы пользователя. В датасете для дообучения, как правило, встречаются новые ключи для уже имеющихся фичей (простейший пример - новый айдишник товара). Из-за отсутствие операции вставки во время обучения приходится заново переваривать 100+ словарей под каждое дообучение, придумывать какую-то эвристическую логику для вставки ключей вне обучения модели
* **Рост датасета**. Классический подход со словарем предполагает, что мы пытаемся заранее посмотреть на весь датасет разом и понять, какие нам фичи нужны, а какие нет. Такой подход на самом деле противоречит end2end концепции: гораздо лучше и удобнее подавать в модель вообще все и иметь механизмы отбора фичей на уровне самой модели. Так, модель может сама определять нужный ей набор эмбеддингов в каждый момент времени. Такие механизмы предполагают наличие не только вставки, но и удаления эмбеддинга из обучения

Библиотека ads_pytorch предлагает ряд наработок, решающих эти проблемы. Фундаментом для всех наработок является слой HashEmbedding

## HashEmbedding
HashEmbedding - прямой аналог torch.nn.EmbeddingBag с несколькими важными отличиями:
1. Под капотом - честная хеш таблица, в которой ключом является произвольный uint64, значением - вектор произвольной размерности
2. Эмбеддинги хранятся в RAM и считаются на CPU, дабы экономить GPU память под более полезные вещи
3. Оптимизированная правильно распараллеленная реализация на C++, на порядки превосходящая CPU реализацию torch.nn.EmbeddingBag
4. Операция вставки: новые эмбеддинги вставляются прямо во время обучения в ```optimizer.step()```
5. Собственные алгоритмы оптимизации, например, [rmsprop_norm](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/hash_embedding/optim.py?rev=r7742332#L206). Работают в несколько раз быстрее стандартных алгоритмов типа adam и экономят память (стандартные adam'ы, впрочем, у нас тоже есть)
6. Механизмы фильтрации хеш-таблицы: вероятностное добавление, удаление неиспользуемых ключей, **future** L1-регуляризация

Высокоуровнево, для работы с HashEmbedding нужно просто превратить ваши категориальные фичи в последовательность uint64 ключей. Готовить заранее словарь не нужно.

### Формат входных данных
HashEmbedding принимает на вход два тензора: тензор айдишников фичей типа int64 и тензор длин объектов типа int32.

```python
for i, feaid in enumerate([1, 2, 3, 4, 5, 67, 458476, 478273409843]): # this is 'vocabulary'
    item = AdamItem(3)
    item.w = torch.FloatTensor([i] * 3)
    hash_table.insert_item(feaid, item)
    
# feaid			/	item.w
# 1				/	[0, 0, 0]
# 2				/	[1, 1, 1]
# 3				/	[2, 2, 2]
# ...
# 478273409843	/	[7, 7, 7]

data = torch.LongTensor([1, 2, 3, 4, 5, 67, 458476, 1, 478273409843]) # this is concrete sample, using ids from 'vocabulary'
data_len = torch.IntTensor([3, 4, 2])

hash_table(data, data_len, compute_mode="sum")
 
# then sum of first 3 embeddings in data would be
# [3, 3, 3] = ([0, 0, 0] + [1, 1, 1] + [2, 2, 2])
#
# the last group is (1, 478273409843), their embeddings are [0, 0, 0] and [7, 7, 7], so the sum is [7, 7, 7]

tensor([[3., 3., 3.],                          # 1 + 2 + 3
        [22., 22., 22.],                       # 4 + 5 + 6 + 7
        [7., 7., 7.]], requires_grad=True)     # 1 + 8
```

### compute_mode

Внимательный читатель заметил в примере выше аргумент ```(python) compute_mode="sum"```.

В HashEmbedding есть два режима вычислений (последний аргумент в forward):
* ```sum``` - суммирует эмбеддинги

* ```mean``` - средний эмбеддинг (sum / кол-во эмбедов в фиче, равное чиселке в data_len тензоре)

  (_в примере ниже используются эмбединги отличные от кода выше_)

```
In [13]: embed(torch.LongTensor([1, 2, 3]), torch.IntTensor([2, 1]))  # default is "sum"
Out[13]:
tensor([[ 0.0130,  0.0004, -0.0123],
        [ 0.0128, -0.0051, -0.0048]], requires_grad=True)

In [15]: embed(torch.LongTensor([1, 2, 3]), torch.IntTensor([2, 1]), compute_mode="mean")
Out[15]:
tensor([[ 0.0065,  0.0002, -0.0062],
        [ 0.0128, -0.0051, -0.0048]], requires_grad=True)
```

### Последовательности эмбеддингов
Зачастую полезно не просто посчитать двумерный BagOfWords, а вычислить N-мерный тензор, в котором последняя размерность - эмбеддинг.
Например, при обучении RNN/Transformer нужен трехмерный тензор размерности (batch_size, sequence_size, embedding_dim). ads_pytorch поддерживает выходные тензоры-эмбеддинги произвольных размерностей.

Рассмотрим пример (взят из тестов https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/tests/hash_embedding/test_hash_embedding.py?rev=7149351#L88):
```python
hash_table = HashEmbedding(AdamEmbeddingHashTable(dim))
# This method of inserting features is nice only for testing or playgrounds
# Insertion in optimizer while training works much faster in C++
for i in range(6):
    item = AdamItem(dim)
    item.w = torch.FloatTensor([i] * dim)
    hash_table.insert_item(i, item)

data = torch.LongTensor([1, 2, 1, 3, 4, 3, 4, 1, 5, 2, 4, 5, 3])
data_len = torch.IntTensor([[1, 1, 3], [1, 1, 1], [1, 1, 0], [2, 0, 1]])
res = hash_table.forward(data, data_len, compute_mode="sum")

reference = torch.FloatTensor([
    [
        [1] * dim,
        [2] * dim,
        [8] * dim  # sum of 1 + 3 + 4
    ],
    [
        [3] * dim,
        [4] * dim,
        [1] * dim
    ],
    [
        [5] * dim,
        [2] * dim,
        [0] * dim
    ],
    [
        [9] * dim,  # sum of 4 + 5
        [0] * dim,
        [3] * dim
    ]
])
assert torch.allclose(res, reference)
```

### Обобщенный код любых вычислений внутри HashEmbedding
Вот код, эквивалентный тому, что происходит в C++ коде для эмбеддингов, для трехмерного выходного тензора
```python
M = 3  # ur seq len
N = 4  # batch size
dim = 5  # embedding_dim
data = torch.LongTensor([1, 2, 1, 3, 4, 3, 4, 1, 5, 2, 4, 5, 3])
data_len = torch.IntTensor([[1, 1, 3], [1, 1, 1], [1, 1, 0], [2, 0, 1]])
assert data_len.sum() == data.numel()
assert data_len.size() == (N, M)
result = torch.zeros(N, M, dim)
compute_mode = "sum"

# Это эквивалентно заполнению хеш-мапы выше
embedding: Dict[int, torch.Tensor] = {key: torch.full((dim, ), fill_value=float(key)) for key in data.tolist()}

# Вот этот код "в лоб" обобщается на любые data_len тензоры: вложенный цикл по каждой размерности
data_offset = 0
for i in range(N):
    for j in range(M):
        # Значения в data_len - сколько эмбеддингов нужно сагрегировать в данной ячейке тензора
        # Мотивация - та же, что у авторов torch.nn.EmbeddingBag: такой код работает сильно быстрее, чем отдельное суммирование
        cur_obj_count = data_len[i][j]
        for obj_offset in range(cur_obj_count):
            feature_id = int(data[data_offset])
            result[i][j] += embedding[feature_id]
            data_offset += 1
        if compute_mode == "mean":
            result[i][j] /= max(cur_obj_count, 1)

# result
tensor([[[1., 1., 1., 1., 1.],
         [2., 2., 2., 2., 2.],
         [8., 8., 8., 8., 8.]],

        [[3., 3., 3., 3., 3.],
         [4., 4., 4., 4., 4.],
         [1., 1., 1., 1., 1.]],

        [[5., 5., 5., 5., 5.],
         [2., 2., 2., 2., 2.],
         [0., 0., 0., 0., 0.]],

        [[9., 9., 9., 9., 9.],
         [0., 0., 0., 0., 0.],
         [3., 3., 3., 3., 3.]]])
```

Обратите особое внимание на то, как именно обходится data_len тензор и как достаются фичи из data, это знание необходимо при варке данных.

## BaseEmbeddingModel и IDeployableModel
BaseEmbeddingModel - это более высокоуровневая абстракция над эмбеддингами. В 99% случаев конечные пользователи должны работать именно с ней. BaseEmbeddingModel - это объединение **всех эмбеддингов в обучении в единый слой**. Такое объединение дает возможность:
1. Удобно шарить словари между различными категориальными фичами
2. Оптимизировать вычисление эмбеддингов
3. Разработчикам библиотеки - добавлять новые фичи в эмбеддинги. Пользователям нужно будет лишь поменять конфиг для фабрики, чтобы опробовать новые наработки

IDeployableModel - базовый класс для слоя с эмбеддингами, который можно будет потом задеплоить в аркадийный C++ inference.

BaseEmbeddingModel имеет мало смысла в отрыве от IDeployableModel (и наоборот), поэтому рассматриваем их вместе. Лучшим примером здесь будет end2end код построения простенького DSSM.

```(python)
from typing import Dict, Union, List, Any

from ads_pytorch.nn.module.base_embedding_model import (
    BaseEmbeddingModel,
    FeatureOrderHolder,
    EmbeddingDescriptor,
    EmbeddingComputeDescriptor,
    embedding_descriptors_to_dim_dict
)
from ads_pytorch.deploy.deployable_model import (
    IDeployableModel,
    TorchModuleDeployDescriptor,
    ParameterServerModelDeployDescriptor
)
import torch


# Это игрушечная архитектура. Для боевых запусков в качестве feed-forward нейросети, выдающей эмбеддинги,
# используйте
# ads_pytorch.nn.module.densenet.WeightNormalizedEmbeddingNetwork
class EmbeddingNetwork(torch.nn.Module):
    def __init__(
        self,
        feature_order_holder: FeatureOrderHolder,
        features: List[str],
        deep_net: torch.nn.Module
    ):
        super(EmbeddingNetwork, self).__init__()
        self.feature_order_holder = feature_order_holder
        self.features = features
        self.deep_net = deep_net

    def forward(self, inputs: List[torch.Tensor]) -> torch.Tensor:
        inputs = [inputs[i] for i in self.feature_order_holder.get_ids(self.features)]
        tensor = torch.cat(inputs, dim=1)
        return self.deep_net(tensor)


# Вообще говоря, код обучения библиотеки поддерживает произвольные torch.nn.Module, равно как и произвольные форматы входов
# Однако, только IDeployableModel может быть из коробки экспортирован в C++ код inference, так что предлагается использовать именно его
class DSSM(IDeployableModel):
    def __init__(
        self,
        embedding_model: BaseEmbeddingModel,
        query: EmbeddingNetwork,
        document: EmbeddingNetwork
    ):
        super(DSSM, self).__init__(embedding_model=embedding_model)
        self.query = query
        self.document = document

        self.alpha = torch.nn.Parameter(torch.ones(1))
        self.bias = torch.nn.Parameter(torch.zeros(1))

    def deployable_model_forward(self, embedded_inputs: List[torch.Tensor]) -> Any:
        query = self.query(embedded_inputs)
        document = self.document(embedded_inputs)

        # Предполагаем, что если вам нужна нормализация выходных векторов, то она делается внутри соответствущих подсетей
        return self.alpha + (query * document).sum(dim=1) + self.bias

    # Пример того, как задеплоить две архитектуры. Деплой рассмотрим подробнее ниже
    def get_serializable_models(self) -> Dict[str, Union[TorchModuleDeployDescriptor, ParameterServerModelDeployDescriptor]]:
        return {
            "query": ParameterServerModelDeployDescriptor(
                features_order=self.query.features,
                model=self.query
            ),
            "document": ParameterServerModelDeployDescriptor(
                features_order=self.document.features,
                model=self.document
            )
        }


def build_feed_forward_impl(in_features: int, out_features: int) -> torch.nn.Module:
    return torch.nn.Sequential(
        torch.nn.Linear(in_features=in_features, out_features=in_features),
        torch.nn.ReLU(),
        torch.nn.LayerNorm(in_features),
        torch.nn.Linear(in_features=in_features, out_features=out_features)
    )


if __name__ == '__main__':
    final_embedding_dim = 50

    # Декларативное описание ВСЕХ эмбеддингов в модели. Согласно интерфейсу IDeployableModel,
    # в модели должен быть *ровно один* центральный BaseEmbeddingModel, насчитывающий все фичи
    embedding_model = BaseEmbeddingModel(
        embeddings=[
            # Один EmbeddingDescriptor описывает одну хеш-таблицу с эмбеддингами
            # Отметим, что необходимо указывать алгоритм оптимизации. В отличие от обычных торчовых слоев,
            # здесь стейт оптимайзера хранится рядом с весами, чтобы не делать отдельную хешмапу
            # с кучей бакетов и лишними указателями
            EmbeddingDescriptor(
                name="Categories",
                # Данная хеш-таблица будет использована для этих категориальных фичей
                features=["QueryCategory", "DocumentCategory"],
                dim=4,  # размерность эмбеддинга
                algo_type="adam"  # adam - отличный дефолт, но жирный по памяти. SOTA - rmsprop_norm
            ),
            EmbeddingDescriptor(
                name="Texts",
                features=[
                    # Каждая фича, записанная строчкой, конвертится в
                    # EmbeddingComputeDescriptor(feature=<name>, compute_mode="mean")
                    # С помощью EmbeddingComputeDescriptor, можно управлять всеми фича-специфичными параметрами
                    # эмбедов конкретной фичи.
                    EmbeddingComputeDescriptor(
                        feature="DocumentText",
                        compute_mode="mean",
                        # Будем добавлять новую фичу с вероятностью 0.2, потому что в полных текстах бывает
                        # редкий уникальный мусор
                        add_prob=0.2,
                    ),
                    # Остальные фичи с дефолтными настройками
                    "DocumentTitle",
                    "QueryText"
                ],
                dim=7,
                algo_type="adam"
            ),
        ],
        # *External* - все фичи, которые мы насчитали извне и которым не нужно проходит через эмбеддинг слои
        external_factors=["DocumentCounters"]
    )

    # Прежде чем переходить к описанию глубоких моделей, разберемся с форматом входа. Поскольку BaseEmbeddingModel
    # должен лежать в основе любых моделей, то и формат входа нужно подгонять именно под него

    def build_inputs(batch_size: int) -> Dict[str, Union[torch.Tensor, List[torch.Tensor]]]:
        # Формат входов на самом деле простой: это словарь строка ->:
        # 1. Если фича external, то будет просто тензор
        # 2. Если фича категориальная, то будет список либо из [data, data_len], либо из [data, data_len, weight] тензоров
        # [data, data_len, weight] - это взвешенный BoW

        def build_randcat_2dim(batch_size: int):
            return [
                torch.randint(100000, size=(batch_size,), dtype=torch.int64),  # data
                torch.tensor([1] * batch_size, dtype=torch.int32)  # data_len
            ]

        def build_randexternal_2dim(batch_size: int, dim: int):
            return torch.randn((batch_size, dim), dtype=torch.float32)

        return {
            "QueryText": build_randcat_2dim(batch_size=batch_size),
            "QueryCategory": build_randcat_2dim(batch_size=batch_size),
            "DocumentTitle": build_randcat_2dim(batch_size=batch_size),
            "DocumentText": build_randcat_2dim(batch_size=batch_size),
            "DocumentCategory": build_randcat_2dim(batch_size=batch_size),
            "DocumentCounters": build_randexternal_2dim(batch_size=batch_size, dim=20)
        }
    inputs_example = build_inputs(batch_size=3)

    # BaseEmbeddingModel выдает...не словарь, а список тензоров
    # Многие применялки в C++ орудуют именно массивами тензоров, а не хеш-таблицами
    # Если в каждом слое использовать хеш-мапы, то для небольших батчей и слоев оверхед на лукапы может быть
    # сравним с вычислением самого слоя. А поскольку мы целимся в highload рекомендательные системы,
    # у нас каждая милисекунда на счету.
    # Однако, при экспериментах интерфейсно все модули должны орудовать именованными фичами,
    # а не индексами в хрен пойми каком массиве. При 100+ фичах такое становится невозможно читать.
    # В качестве компромисса мы предлагаем FeatureToOrderHolder. Суть в том, чтобы все-все-все слои
    # в конструкторе содержали ссылку на объект-холдер с порядком фичей. Аналогичная логика повторена
    # в C++, с той лишь разницей, что в C++ превращение строковых фичей в индексы массива происходит
    # заранее в конструкторах, оптимизируя лукапы на inference
    embedding_outputs: List[torch.Tensor] = embedding_model(inputs_example)

    feature_holder: FeatureOrderHolder = embedding_model.get_feature_order_holder()

    # Допустим, мы хотим достать фичу x. Пишем
    print(embedding_outputs[feature_holder.get_ids(["QueryText"])[0]])

    # Или несколько фичей
    print([embedding_outputs[i] for i in feature_holder.get_ids(["QueryText", "QueryCategory"])])

    # Распишем один раз ручками forward-pass для примера:
    _partial_manual_outputs = {
        # Эмбедим тексты
        "QueryText": embedding_model.embeddings["Texts"](*inputs_example["QueryText"]),
        "DocumentTitle": embedding_model.embeddings["Texts"](*inputs_example["DocumentTitle"]),
        # И не забываем про add_prob из дексриптора
        "DocumentText": embedding_model.embeddings["Texts"](*inputs_example["DocumentText"], add_prob=0.2),

        # Эмбедим категории
        "QueryCategory": embedding_model.embeddings["Categories"](*inputs_example["QueryCategory"]),
        "DocumentCategory": embedding_model.embeddings["Categories"](*inputs_example["DocumentCategory"]),

        # все external фичи просто форвардим наверх
        "DocumentCounters": inputs_example["DocumentCounters"]
    }
    _list_manual_outputs = [_partial_manual_outputs[x] for x in feature_holder.get_order()]
    for t1, t2 in zip(embedding_outputs, _list_manual_outputs):
        assert torch.allclose(t1, t2)

    # Глобальная цель такая: сделать консистентный с C++ библиотеками inference интерфейс, не ударив по удобству
    # 1. Фабрики-конструкторы модулей оперируют строковыми списками фичей => наглядность и
    # удобство построения моделей не страдает
    # 2. forward орудует массивами тензоров => заставляем пользователя сразу писать код так, чтобы слой
    # можно было без проблем задеплоить в плюсы
    # 3. Чтобы достать фичу, нужно написать... на 30 символов больше, чем лукап в словарь.
    # Мы решили, что это достойный компромисс

    # Окей, вернемся к построению моделей

    query_embeddings = [
        "QueryText",
        "QueryCategory"
    ]
    query_external = {}

    document_embeddings = [
        "DocumentTitle",
        "DocumentText",
        "DocumentCategory"
    ]

    document_external = {
        "DocumentCounters": 20
    }

    dim_dict = embedding_descriptors_to_dim_dict(embedding_descriptors=embedding_model.embedding_descriptors)

    # Передаем наш feature_order_holder во все модельки
    document_network = EmbeddingNetwork(
        feature_order_holder=embedding_model.get_feature_order_holder(),
        features=document_embeddings + list(document_external.keys()),
        deep_net=build_feed_forward_impl(
            in_features=sum(dim_dict[name] for name in document_embeddings) + sum(document_external.values()),
            out_features=final_embedding_dim
        )
    )

    query_network = EmbeddingNetwork(
        feature_order_holder=embedding_model.get_feature_order_holder(),
        features=query_embeddings + list(query_external.keys()),
        deep_net=build_feed_forward_impl(
            in_features=sum(dim_dict[name] for name in query_embeddings),
            out_features=final_embedding_dim
        )
    )

    dssm = DSSM(
        embedding_model=embedding_model,
        query=query_network,
        document=document_network
    )

    inputs = build_inputs(batch_size=10)
    prediction = dssm(inputs)
    print(prediction)
```

# Фабрики моделей
Окей, вот тут мы уже запилим нечто посерьезнее. На самом деле, марахайка с ```FeatureOrderHolder``` разрабатывалась под сложные вложенные нейросети.

Поскольку рекомендательными системами в Яндексе обычно занимаются бекендеры, а не специально выделенные дата сатанисты, основной формат описания сложных вложенных моделей должен подходить под самый популярный и наиболее прокачанный скилл бекендеров: умение перекладывать json.

## BaseEmbeddingModel json
Думаю, здесь пример будет лучше 1000 слов.

Вот такой вот json конфиг
```(json)
"features": {
    "external": [
        "CountersAggregatedValues",
        "BigBQueryFactors",
    ],
    "embeddings": {
        "default_algo": "rmsprop_norm",
        "default_algo_params": {
            "lr": 0.0003,
            "expiration_ttl": 336
        },
        "features": [
            {
                "dim": 64,
                "name": "UserRegionID"
            },
            {
                "dim": 64,
                "name": "UserBestInterests",
                "algo": "adam"
            },
            {
                "dim": 72,
                "name": "AffinitiveSites",
                "features": [
                    "KryptaTopDomain",
                    {"name": "UserCryptaAffinitiveSitesIDs", "add_prob": 0.1}
                ]
            },
            {
                "dim": 64,
                "name": "QueryTexts",
                "features": [
                    "BigBQueryTexts",
                    "QueryHistoryTexts",
                    "SearchQueryTextTokenLemma"
                ],
                "add_prob": 0.3
            },
            {
                "dim": 64,
                "name": "Urls",
                "features": [
                    "LandingPageUrl",
                    {"name": "BannerUrl", "add_prob": 0.2},
                ],
                "add_prob": 0.3
            }
        ]
    }
}
```


преобразуется вот в такой python код

```(python)

    model = BaseEmbeddingModel(
        external_factors=[
            "CountersAggregatedValues",
            "BigBQueryFactors",
        ],
        embeddings=[
            EmbeddingDescriptor(
                name="UserRegionID",
                features=["UserRegionID"],
                dim=64,
                algo_type="rmsprop_norm"
            ),
            EmbeddingDescriptor(
                name="UserBestInterests",
                features=["UserBestInterests"],
                dim=64,
                algo_type="adam"
            ),
            EmbeddingDescriptor(
                name="AffinitiveSites",
                features=[
                    "KryptaTopDomain",
                    EmbeddingComputeDescriptor(
                        feature="UserCryptaAffinitiveSitesIDs",
                        add_prob=0.1
                    )
                ],
                dim=72,
                algo_type="rmsprop_norm"
            ),
            EmbeddingDescriptor(
                name="QueryTexts",
                features=[
                    EmbeddingComputeDescriptor(
                        feature="BigBQueryTexts",
                        add_prob=0.3
                    ),
                    EmbeddingComputeDescriptor(
                        feature="QueryHistoryTexts",
                        add_prob=0.3
                    ),
                    EmbeddingComputeDescriptor(
                        feature="SearchQueryTextTokenLemma",
                        add_prob=0.3
                    )
                ],
                dim=64,
                algo_type="rmsprop_norm"
            ),
            EmbeddingDescriptor(
                name="Urls",
                features=[
                    EmbeddingComputeDescriptor(
                        feature="LandingPageUrl",
                        add_prob=0.3
                    ),
                    EmbeddingComputeDescriptor(
                        feature="BannerUrl",
                        add_prob=0.2
                    ),
                ],
                dim=64,
                algo_type="rmsprop_norm"
            ),
        ]
    )
```


## SubNetworks
###  Рекурсивное пострение глубоких архитектур
Здесь надо будет поглубже погрузиться в формат описания глубоких частей моделей. Глубокая часть - все параметры, кроме эмбеддинг слоев.

У каждой нейросети есть два опциональных словарика: ```sub_networks``` и ```normalizers```:
* ```normalizers``` - это простые подсети с одним входом и одним выходом, которые **подменяют своим выходом фичу**
* ```sub_networks``` - это сложные подсети с произвольным набором входов.

Обобщенный код составления подсетей выглядит как-то так:

```(python)
class MyModuleWithNorm(torch.nn.Module):
    def __init__(
        self,
        feature_holder: FeatureOrderHolder,
        features: List[str],
        normalizers: Dict[str, torch.nn.Module],
        sub_networks: Dict[str, torch.nn.Module]
    ):
        super(MyModuleWithNorm, self).__init__()
        self.normalizers = torch.nn.ModuleDict(normalizers)
        self.sub_networks = torch.nn.ModuleDict(sub_networks)
        self.feature_holder = feature_holder
        self.features = features[:]

    def forward(self, embedding_inputs):
        # Сначала считаем подсети на чистых ненормализованных входах чтобы избежать сайд-эффектов.
        # По здравому смыслу, мы должны вычислять сети с самых нижних слоев,
        # но, к сожалению, при рекурсивном конструировании модели входы будут подаваться сначала в самый верхний слой
        sub_network_outputs = {
            # Мы всегда подаем весь список embedding_inputs в подсети. Это автоматически означает, что любая
            # подсеть должна оперировать тем же feature_holder'ом
            name: module(embedding_inputs)
            for name, module in self.sub_networks.items()
        }

        # Нормализовываем входы. Нормалайзеров на подсети нет - считаем, что если нужно,
        # нормализацию можно сделать в подсети
        inputs = []
        for name, idx in zip(self.features, self.feature_holder.get_ids(self.features)):
            tensor = embedding_inputs[idx]
            if name in self.normalizers:
                tensor = self.normalizers[name](tensor)
            inputs.append(tensor)

        # Юзер делает с этим добром все что хочет
        return self._forward_impl(sub_network_outputs=sub_network_outputs, normalized_inputs=inputs)

    def _forward_impl(self, sub_network_outputs, normalized_inputs):
        raise NotImplementedError
```

Отметим, что базовый класс с такой вот логикой мы решили не делать, так как сразу начинали сыпаться всякие краевые случаи. Оставляем это правило на откуп пользователю. В ads_pytorch есть некий набор "общих" подсетей, где такая логика строго проверяется и ревьюится. В своих слоях можете делать что хотите.

Боевой пример: fully-connected сеть с подсетью-трансформером
```(python)
import torch
from typing import List, Dict
from ads_pytorch.nn.module.base_embedding_model import FeatureOrderHolder


class FeedForward(torch.nn.Module):
    def __init__(
        self,
        feature_holder: FeatureOrderHolder,
        features: List[str],
        normalizers: Dict[str, torch.nn.Module],
        sub_networks: Dict[str, torch.nn.Module],
        deep: torch.nn.Module
    ):
        super(FeedForward, self).__init__()
        self.normalizers = torch.nn.ModuleDict(normalizers)
        self.sub_networks = torch.nn.ModuleDict(sub_networks)
        # Заранее селектим себе порядок, в котором будем конкатенировать подсети
        # В "боевых" аналогах feed-forward сетей этот порядок сохраняется и загружается из state_dict
        # модели, чтобы исключить ситуации, когда пользователь подает в конструктор словарик
        # с измененным порядком ключей (в PY3.6+ все словари ordered) и пытается подгрузить сохраненную модель
        # при обучении которой порядок конкатенации был другой
        # В нашем примере мы опустим написание функций state_dict/load_state_dict
        self.sub_networks_order = list(self.sub_networks.keys())
        self.feature_holder = feature_holder
        self.features = features[:]
        self.deep = deep

    def forward(self, embedding_inputs: List[torch.Tensor]) -> torch.Tensor:
        sub_network_outputs = {
            name: module(embedding_inputs)
            for name, module in self.sub_networks.items()
        }

        inputs = []
        for name, idx in zip(self.features, self.feature_holder.get_ids(self.features)):
            tensor = embedding_inputs[idx]
            if name in self.normalizers:
                tensor = self.normalizers[name](tensor)
            inputs.append(tensor)

        deep_input = torch.cat(inputs + [sub_network_outputs[name] for name in self.sub_networks_order], dim=1)
        return self.deep(deep_input)


class TransformerSubnetwork(torch.nn.Module):
    def __init__(
        self,
        feature_holder: FeatureOrderHolder,
        features: List[str],
        normalizers: Dict[str, torch.nn.Module],
        sub_networks: Dict[str, torch.nn.Module],
        encoder_impl: torch.nn.TransformerEncoder
    ):
        super(TransformerSubnetwork, self).__init__()
        assert len(sub_networks) == 0
        self.normalizers = torch.nn.ModuleDict(normalizers)
        self.features = features[:]
        self.feature_holder = feature_holder
        self.encoder_impl = encoder_impl

    def forward(self, embedding_inputs: List[torch.Tensor]):
        inputs = []
        for name, idx in zip(self.features, self.feature_holder.get_ids(self.features)):
            tensor = embedding_inputs[idx]
            if name in self.normalizers:
                tensor = self.normalizers[name](tensor)
            inputs.append(tensor)

        # В нашем примере опускаем технические детали вида "а если пустота", "а если маска" и т.д.
        transformer_input = torch.cat(inputs, dim=2)  # 3-dim тензор
        transformer_output = self.encoder_impl(transformer_input)
        return torch.mean(transformer_output, dim=0)  # average along sequence_len dimension


if __name__ == '__main__':
    # Забьем на BaseEmbeddingModel
    feature_holder = FeatureOrderHolder({"SearchQueryHistory": 0, "UserID": 1, "BannerID": 2})

    transformer = TransformerSubnetwork(
        feature_holder=feature_holder,
        features=["SearchQueryHistory"],
        normalizers={},
        sub_networks={},
        encoder_impl=torch.nn.TransformerEncoder(
            encoder_layer=torch.nn.TransformerEncoderLayer(
                d_model=512,
                nhead=8
            ),
            num_layers=10
        )
    )

    feed_forward = FeedForward(
        feature_holder=feature_holder,
        features=[
            "UserID",
            "BannerID"
        ],
        normalizers={},
        sub_networks={
            "query_history": transformer
        },
        deep=torch.nn.Linear(512 + 64 + 64, 1)
    )

    inputs = [
        # torch.nn.TransformerEncoder accepts (sequence_len, batch_size, embedding_dim)
        # в ads_pytorch реализации трансформеров берут (batch_size, sequence_len, embedding_dim)
        torch.randn(50, 10, 512),  # SearchQueryHistory
        torch.randn(10, 64),       # UserID
        torch.randn(10, 64)        # BannerID
    ]

    print(feed_forward(inputs))
```

### Конфигурирование фабрик архитектур. Библиотека архитектур
Конфигурирование глубоких архитектур из json делается рекурсивно от самого верхнего слоя к нижним. [Библиотека с новыми фабриками](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2). Общие механизмы рекуррентного создания моделей описаны тут:
* [network_factory.py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2/network_factory.py) - создание нейросетей и подсетей
* [normalizer_factory.py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2/normalizer_factory.py) - создание нормалайзеров

Фабрики подразумевают расширение и регистрацию новых модулей. Для этого нужно просто написать свою фабричную функцию и обернуть ее в декоратор, вот так
```(python)
from densenet_tsar_query_attention_v2.normalizer_factory import register_normalizer_factory
from densenet_tsar_query_attention_v2.network_factory import register_network_factory

@register_normalizer_factory("dummy_normalizer_identity")
def _build_identity_normalizer(cfg: Dict[str, Any]):
    return torch.nn.Identity()


@register_network_factory("dummy_linear")
def generic_feed_forward_builder_impl(
    cfg: Dict[str, Any],
    sub_networks: Dict[str, torch.nn.Module],
    normalizers: Dict[str, torch.nn.Module],
    embedding_descriptors: List[EmbeddingDescriptor],
    feature_order_holder,
    unique_prefix: str
) -> FeedForward:
    return FeedForward(
        feature_order_holder=feature_order_holder,
        sub_networks=sub_networks,
        normalizers=normalizers,
        features=cfg["features"],
        deep=torch.nn.Linear(1000, 1)
    )
```

И можно будет потом эти сети создавать из конфигов
```(json)
{
    "user": {
        "network_type": "dummy_linear",
        "features": [
            "UserID",
            "UserSocDem",
            "UserTopCategories",
            "CountersAggregated"
        ],
        "normalizers": {
            "CountersAggregated":{
                "type": "dummy_normalizer_identity"
            }
        },
        "sub_networks": {
            "QueryTransformer": {
                "network_type": "transformer_encoder",
                "embeddings": [
                    "QueryTexts"
                ]
            }
        }
    }
}
```

Единственное ограничение - фабрики должны быть зарегистрированы до того, как вы будете читать конфиг. Обычно тут два случая:
1. Библиотечный слой, покрытый тестами и довольно общий, он пишется в саму библиотеку ```densenet_tsar_query_attention_v2``` и регистрируется при импорте библиотеки в ```__init__.py```
2. Пользовательский экспериментальный слой, описанный прямо в скрипте обучения. В этом случае декоратор точно отработает на запуске скрипта до конструирования модельки

### Библиотечные слои
Здесь описаны *важные* слои, покрытые юнит тестами и достаточно абстрактные для общего пользования. Разработчики ads_pytorch гарантируют обратную совместимость для этих слоев

#### [GenericFeedForwardWithNormalizers](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2/generic_feed_forward_with_normalizers.py?rev=r8036830)
Обертка над произвольной feed-forward нейросетью. Под feed-forward нейросетью здесь подразумевается нейросеть с одним тензором на вход и одним на выход, причем входной тензор **двумерный**.

В принципе, ничего ценного, кроме интерфейсов, там нет. Все sub_networks должны быть наследниками [SingleMatrixOutputMixin](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/nn/module/single_matrix_output_network.py), говорящей, что:
1. Ваш слой выдает одну матрицу на выходе
2. У слоя есть метод, по которому можно заранее узнать число колонок на выходе

Эти интерфейсы позволяют автоматически инферить размер входного слоя для fully-connected сети. В качестве реализации feed-forward сети, есть [два базовых слоя](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2/generic_feed_forward_factory.py?rev=r8036830#L52):
* DenseNetEmbeddingNetwork - хорошо знакомые concat-слои из DSSM.
* WeightNormalizedEmbeddingNetwork - улучшение DenseNet сети, позволяющее учить норму вектора и не использовать косинусное расстояние. Дает больше профита, чем аналогичная по числу параметров DenseNet сеть на большинстве задач. **Должен быть дефолтом**

[пример конфига](https://a.yandex-team.ru/arc/trunk/arcadia/junk/alxmopo3ov/ad_transformer_v2/warmup_without_deep_part_long/config.json?rev=r7915854#L234)

#### [GenericFeedForwardWithHeads](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2/generic_feed_forward_with_normalizers.py?rev=r8409022#L196)
Представляет собой расширение функционала GenericFeedForwardWithNormalizers с возможностью обучения многоголовой сети.
На вход принимается shared_deep - общая для всех голов глубока часть, которая должна являться SingleMatrixOutputMixin,
вход у нее аналогичен GenericFeedForwardWithNormalizers - конкатенация общей части эмбеддингов (об этом далее) и выходов подсетей.

Получившаяся двумерная матрица является промежуточным состоянием, которое после некоторых модификаций подается на вход моделям-головам.
* Первая возможная модификация - использование части эмбеддинга только в модели-голове, чтобы эта часть выучивала какое-то специфическое для данной головы представление.
Для этого перед подачей в общую глубокую модель часть эмбеддинга отделяется и не используется в общей глубокой модели,
а конкатенируется с промежуточным состоянием перед подачей в модель-голову.
Регулируется это флагом "split_embeddings" в конфиге и полем "embedding_ratio" в конфиге головы,
которое говорит какую часть размерности эмбеддингов отделять и использовать в голове.
* Вторая возможная модификация - сжатие входных фичей. Она специфична для денснета в качестве общей глубокой модели и позволяет отделить от выхода денснета его вход,
сжать этот вход и конкатенировать обратно, таким образом уменьшая ширину слоев в модели-голове. За это отвечает "input_compression_impl" в конфиге головы.

[пример конфига](https://a.yandex-team.ru/arc/trunk/arcadia/junk/ya-philya/multitarget/pclick_conv/splitted_models_splitted_embeds_conf.json?rev=r8407110#L499)

#### [MultisequenceTransformerEncoder2](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/densenet_tsar_query_attention_v2/densenet_tsar_query_attention_v2/multisequence_transformer_encoder2.py)
Обертка над трансформером в библиотеке ads_pytorch. MultiSequence означает, что этот слой позволяет объединять в одну "последовательность" различные источники данных. Последовательностью в классическом смысле это перестает быть, но ведь мы все знаем, что transformer encoder - тулза для работы над неупорядоченным множеством, а упорядоченность, "последовательноность" и т.д. вводится дополнительными хаками.

Начнем с простого примера одной последовательности ([таблица с фичами](https://yt.yandex-team.ru/hahn/navigation?path=//home/ads/tzar/docs/plain_sum_multisequence_transformer_encoder2_history_keys)):
```json
"sub_networks": {
    "NeuralCounterByAdGroup": {
        "network_type": "multisequence_transformer_encoder2",
        "transformer_type": "ads_pytorch",
        "attention": "linear_symmetric",
        "linear_type": "orthogonal",
        "d_model": 32,
        "num_layers": 3,

        "sub_networks": {
            "UserFeatures": {
                "embeddings": [
                    "HistoryKeys"
                ],
                "realvalue": {
                    "HistoryAge": 1,
                    "HistoryClicks": 1,
                },
                "key_mask": "HistoryLength",
                "max_seq_len": 128,
                "combine_type": "plain_sum",
                "network_type": "multisequence_tranformer_input_sequence_builder"
            }
        },
    }
}
```

Во-первых - **все последовательности описываются в sub_networks**. Каждая sub_network здесь должна выдавать один трехмерный тензор размера (batch_size, sequence_len, embedding_dim). В подавляющем большинстве случаев вам стоит юзать **multisequence_tranformer_input_sequence_builder** и брать имеющиеся **combine_type** либо, в крайнем случае, делать дополнительные combine_type. С выходами всех sub_network происходит следующее:
1. Делается линейная проекция на размерность трансформера ```d_model```
2. Конкатенируются тензоры последовательностей по размерности 1, отвечающей за номер элемента последовательности
3. Конкатенируются ```key_mask``` всех последовательностей
4. Одна сконкатенированная большая последовательность прогоняется через transformer encoder
5. Выходной тензор усредняется с учетом ```key_mask``` по размерности 1 (элементы последовательности). На выходе получаем матрицу

multisequence_transformer_encoder2 является наследником SingleMatrixOutputMixin, а значит - может использоваться как подсеть для GenericFeedForward нейросети.

##### key_mask

```key_mask``` - маскирование не участвующих в Attention'е ключей. Наиболее распространенный случай - маскирование zero padding'а. В одном батче, как правило, последовательности разной длины, поэтому чтобы добить их до одной длины и запихнуть в один трехмерный тензор, "хвосты" просто забивают нулями. Эти нули не должны участвовать в расчете модели, дабы не портить

##### Встроенные типы TransformerEncoder
За выбор типа TransformerEncoder'а отвечает поле ```"transformer_type"```.

###### torch
Классический torch.nn.TransformerEncoder. Параметры:
* ```d_model``` - размерность эмбеддинга в трансформере
* ```num_layers``` - число слоев
* ```num_heads``` - число голов (опциональный, дефлот 1)
* ```dim_feedforward``` - размерность промежуточного слоя между attention'ами (опционален, если не указан, то будет равен d_model)

###### ads_pytorch
[ReZeroTransformerEncoder](https://arxiv.org/abs/2003.04887) с кастомным выбором Attention'ов. Сейчас поддержаны три вида:
1. [SoftmaxAttention](https://arxiv.org/abs/1706.03762), ```"attention_type": "softmax"```
2. [LinearAttention](https://arxiv.org/abs/2006.16236), ```"attention_type": "linear"```
3. [LinearSymmetricAttention](https://st.yandex-team.ru/TORCHPS-405#6075df4ee98305599d6e119a), ```"attention_type": "linear_symmetric"```

Пока не наблюдалось ни одного случая, чтобы linear_symmetric проиграл в качестве обычному linear, но зато он эффективнее по памяти. При выборе линейного трансформера стоит использовать именно его.

Кастомные параметры:
* ```linear_type``` - тип линейного слоя. Может быть либо "orthogonal" - [OrthogonalLinear](https://a.yandex-team.ru/arc/trunk/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/nn/module/orthogonal_linear.py), либо "usual" - ```torch.nn.Linear```

Остальные параметры - d_model, d_feedforward, num_layers, num_heads - аналогичны параметрам torch трансформера.

###### Рекомендуемый TransformerEncoder
```json
{
    "transformer_type": "ads_pytorch",
    "attention": "linear_symmetric",
    "linear_type": "orthogonal"
}
```

##### Встроенные типы построений последовательностей в multisequence_tranformer_input_sequence_builder
За это отвечает параметр ```"combine_type"```. Для **всех** примеров ниже давайте использовать следующие "входы":

```python
import torch
batch_size = 10
seq_len = 256
dim = 64

embeddings = {
    "HistoryKeys": torch.rand(batch_size, seq_len, dim),
    "HistoryPositionalEmbeddings": torch.rand(batch_size, seq_len, dim),
}
realvalue = {
    "HistoryAge": torch.rand(batch_size, seq_len, 1),
    "HistoryStatistics": torch.rand(batch_size, 17)
}
```

а также следующую часть конфига, **общую** для всех примеров ниже
```json
{
    "embeddings": [
        "HistoryKeys",
        "HistoryPositionalEmbeddings"
    ],
    "realvalue": {
        "HistoryAge": 1,
        "HistoryStatistics": 17
    },
    "network_type": "multisequence_tranformer_input_sequence_builder"
}
```

###### plain_sum
Суммирует все эмбеддинги, затем конкатенирует к ним realvalue фичи.

```python
embedding_tensor = sum([
    embeddings["HistoryKeys"],
    embeddings["HistoryPositionalEmbeddings"],
])
result = torch.cat([embedding_tensor] + [realvalue["HistoryAge"], realvalue["HistoryStatistics"]], dim=1)
```

###### "densenet"
Feed-forward нейросеть. Feed-forward будет работать **только по последней размерности**.

```python
from ads_pytorch.nn.module.densenet import DenseNet
densenet = DenseNetEmbeddingNetwork()

inputs = torch.cat(list(embeddings.values()) + list(realvalue.values()), dim=1)
result = densenet(inputs)
```

Есть еще настройка "weightnorm_net" - она жрет **сильно** больше памяти и не дает профита под трансформером. WeightNormalizedEmbeddingNetwork нужен только наверху DSSM'а.

###### Рекомендуемые настройки
Если у вас **немного** различных тензоров-эмбеддингов (скажем, <= 2), то стоит использовать ```plain_sum```. Количество realvalue значения не имеет. В остальных случаях - серебряной пули нет, нужно пробовать и densenet, и plain_sum, и выбирать лучший.
