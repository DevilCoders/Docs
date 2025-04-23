LXC образ для CI
================

Образ для использования в CI.

Как собрать:
Sandbox -> Create -> Task -> type: SANDBOX_LXC_IMAGE

Скопипастить lxc.sh в поле `custom_script`.

В результате получаем ресурс с предустановленными тулами,
который можно использовать как `container_resource` в CI.

Джобы в CI работают в сети `_CMSEARCHNETS_`.
