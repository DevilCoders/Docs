Тест бинарника search/daemons/models_proxy с замоканными источниками.

Суть: есть предзагруженные наборы запросов и ответов прокси вместе с запросами и ответами подысточников,
тестер поднимает mock_subsource на localhost на основе ответов подысточников,
создаёт конфиг среднего, смотрящий на поднятый mock_subsource,
поднимает models_proxy на другом порту localhost в нескольких разных конфигурациях,
стреляет в поднятую models_proxy запросами и сравнивает ответы с каноническими.

Запросы и ответы хранятся в sandbox и описаны в [*.external](https://docs.yandex-team.ru/ya-make/manual/common/data#data_ext).
Их умеет загружать с хамстера search/daemons/models_proxy/tests/generator.
