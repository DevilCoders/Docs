DNS-записи для существующего до [создания зоны](#create-peering-zone) кластера не мигрируют автоматически в эту зону.

Чтобы DNS-записи для такого кластера мигрировали в новую зону, необходимо, чтобы поменялась хотя бы одна DNS-запись во внутренних зонах облачных сетей `cluster-net` и `vm-net`.

Для этого можно, например, создать по одной виртуальной машине в каждой облачной сети. Эти виртуальные машины можно удалить после миграции DNS-записей.

{% if audience != "internal" %}

Но, поскольку [ранее уже были созданы виртуальные машины](#before-you-begin) `cluster-vm` и `other-vm`, для достижения желаемого эффекта достаточно [остановить и затем запустить](../../../compute/operations/vm-control/vm-stop-and-start.md) их.

{% else %}

Но, поскольку [ранее уже были созданы виртуальные машины](#before-you-begin) `cluster-vm` и `other-vm`, для достижения желаемого эффекта достаточно остановить и затем запустить их.

{% endif %}

Когда процесс миграции будет завершен, в зоне с именем `vpc-peering-zone` появятся DNS-записи кластера.

{% note tip %}

Перед миграцией DNS-записей production-кластеров выполните миграцию записей в тестовом каталоге с тестовым кластером. Это позволит убедиться в том, что процесс миграции происходит без ошибок.

{% endnote %}