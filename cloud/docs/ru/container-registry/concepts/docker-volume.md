# Том Docker

_Том Docker_ — это средство для постоянного хранения информации на виртуальной машине. Данные в томе хранятся независимо от контейнеров. Если вы удалите контейнер, то тома и данные в томах останутся. Удаление тома — отдельная операция.

## Тома и Docker Compose {#volume-compose}

Вы можете использовать [Docker Compose]{% if product == "yandex-cloud" %}(../../cos/concepts/coi-specifications.md#compose-spec){% endif %}{% if product == "cloud-il" %}(https://docs.docker.com/compose/compose-file/){% endif %} для создания и управления несколькими томами. При первом вызове `docker-compose up` будут созданы описанные тома. Эти же тома будут использоваться при последующих вызовах.

Если вы запускаете контейнер, который создает новый том, то контент из каталога монтирования будет скопирован в том. Контейнеры, которые смонтируют том себе, получат доступ к данным в томе.