Почему оно так написано и как это читать?

C++ применялка написана на абстракции "слой", а прямой трансфер с помощью torchscript невозможен ввиду отсутствия libtorch в аркадии. Слои принимают на вход и возвращают массивы тензоров, никаких словарей или вложенных структур там не предусмотрено. Чтобы сделать трансфер модели в плюсы максимально прозрачным, мы сделали BaseEmbeddingModel. Он должен быть **один** на каждую деплоящуюся нейросеть и содержать в себе **все** фичи. Смысл следующий: этот embedding model однозначным образом задает порядок фичей (feature_to_id) и мы даем гарантию на воспроизводимость этого порядка в C++. Дальше, на основании этого порядка, можно пилить любые подмодули и маппить настоящие имена фич в айдшники input'ов

* feed_forward_with_embeddings.py - это Banner и Page сети
* user_network.py - User сеть
