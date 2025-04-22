# Schema-registry

`Schema-registry` лежит в аркадии, но в соседней [папке](https://a.yandex-team.ru/arc_vcs/classifieds/schema-registry).
Для интеграции с `verticals-backend` на каждую директорию/файл генерятся bazel-таргеты.
Таргеты можно сгенерить вручную через команду `make gen/schema-registry` или слить PR со схемой и дождаться, пока придет робот и запушит их.
