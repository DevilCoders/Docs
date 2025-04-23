# Geoproduct binaries
[Wiki-страница с более подробным описанием](https://wiki.yandex-team.ru/users/folunin/geoproduct-advert-delivery/)
Бинарники считывают рекламные данные Геопродукта из входных XML ([TYCOON_ADVERTS](https://sandbox.yandex-team.ru/resources?type=TYCOON_ADVERTS), [TYCOON_ADS](https://sandbox.yandex-team.ru/resources?type=TYCOON_ADS)) и заливают их в SaaS.

## Geoproduct indexer
Предназначен для подготовки рекламы Геопродукта к отправке в SaaS.
Обрабатывает входные XML и формирует текстовый файл с отсортированным списком кортежей «permalink, номер бакета, сериализованный и закодированный в base64 protobuf с рекламным патчем метапоиска, md5 рекламного патча»
Ресурс в Sandbox — [GEOPRODUCT_INDEXER_EXECUTABLE](https://sandbox.yandex-team.ru/resources?type=GEOPRODUCT_INDEXER_EXECUTABLE)

## Diff uploader
Предназначен для инкрементальной заливки изменений рекламных данных в SaaS.
Сравнивает файл, в котором записано текущее состояние SaaS, и файл, полученный в результате индексации свежих XML, вычисляет diff и, если он не пуст, то заливает не более заданного числа его элементов в SaaS (а также сохраняет эти изменения в файле с текущим состоянием)
Ресурс в Sandbox — [GEOPRODUCT_DIFF_UPLOADER_EXECUTABLE](https://sandbox.yandex-team.ru/resources?type=GEOPRODUCT_DIFF_UPLOADER_EXECUTABLE)

## Bucket validator
Предназначен для корректировки ошибок при заливке рекламных данных.
Запрашивает из SaaS данные определённого бакета, сравнивает их с данными того же бакета из файла, полученного в результате индексации свежих XML, вычисляет diff и, если он не пуст, то заливает не более заданного числа его элементов в SaaS.
Ресурс в Sandbox — [GEOPRODUCT_BUCKET_VALIDATOR_EXECUTABLE](https://sandbox.yandex-team.ru/resources?type=GEOPRODUCT_BUCKET_VALIDATOR_EXECUTABLE)
