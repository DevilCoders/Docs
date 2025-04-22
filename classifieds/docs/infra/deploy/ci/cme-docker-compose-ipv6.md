# Обеспечение доступа из docker-compose в gitlab-ci до внутренних ресурсов Яндекса

Для того, чтобы пользоваться внутренними ресурсами Яндекса из docker-compose в gitlab-ci, необходимо:

1. Заказать сетевую дырку от гитлаб-билдеров до необходимого ресурса. Сделать это можно через админов в очереди [VASUP](../../support/vasup.md);
2. Подключить ipv6 для docker-compose в используемом пайплайне.

Ниже приведена инструкция, как подключить ipv6 для docker-compose.

## Подключение ipv6 в docker-compose

{% note warning %}

Примеры содержания файлов приведены в конце инструкции.

{% endnote %}

1. Необходимо повысить приоритет ipv6-адресам при резолвинге из docker-compose. Для этого нужно добавить в скрипт, запускаемый в docker-compose, ниже указанную команду:

    `echo "label 2a02::/16 1" >> /etc/gai.conf`

2. Включить в спеке docker-compose ipv6 для используемой сети: `enable_ipv6: true`;
3. Добавить в скрипт пайплайна вычисление уникального id для использования в подсети:

    `export CI_PIPELINE_ID_REMAINDER=$(printf '%x' $(expr $CI_PIPELINE_ID % 65536))`

4. Добавить в спеку docker-compose подсеть, включающую в себя вычисленный в п.3 id:

    `subnet: fd00::${CI_PIPELINE_ID_REMAINDER:-0}:0:0/96`

### Примеры файлов

{% cut "Пример gitlab-ci.yml" %}
```
<...>
test:
  stage: test
  <...>
  script:
    - export CI_PIPELINE_ID_REMAINDER=$(printf '%x' $(expr $CI_PIPELINE_ID % 65536))
<...>
```
{% endcut %}

{% cut "Пример docker-compose-ci.yml" %}
```
version: "3.4"
services:
  redis:
    image: redis:latest
    networks:
      - overlay

  tests:
    image: service-image:${IMAGE_TAG}
    build: .
    restart: always
    depends_on:
      - redis
    networks:
      - overlay
    command: ["./run_tests"]

networks:
  overlay:
    enable_ipv6: true
    ipam:
      config:
        - subnet: fd00::${CI_PIPELINE_ID_REMAINDER:-0}:0:0/96
```
{% endcut %}

{% cut "Пример скрипта run_tests, запускаемого из docker-compose" %}
```
#!/bin/sh

echo "label 2a02::/16 1" >> /etc/gai.conf
<running tests>
```
{% endcut %}
