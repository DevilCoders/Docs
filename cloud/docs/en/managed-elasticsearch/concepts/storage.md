---
title: Elasticsearch Storage Types
description: 'The Elasticsearch service allows you to use network and local storage for clusters. The network storage is implemented on the basis of network blocks, virtual disks in the Yandex Cloud infrastructure.'
keywords:
  - Elasticsearch storage
  - Elasticsearch repositories
  - Elasticsearch
---

# Storage types

{% if audience != "internal" %}

{{ mes-name }} lets you use network and local storage drives for database clusters. Network storage drives are based on network blocks, which are virtual disks in the {{ yandex-cloud }} infrastructure. Local disks are physically located on the cluster servers.

{% include [storage-type-nrd](../../_includes/mdb/mes/storage-type.md) %}

## Specifics of local SSD storage {#local-storage-features}

* Local SSD storage doesn't provide fault tolerance for a single-host cluster: if a disk fails, the data is permanently lost. To ensure fault tolerance, create clusters of three or more hosts and configure index [sharding and replication](scalability-and-resilience.md).
* You are charged for a cluster with this storage type even if it's stopped. Read more in the [pricing policy](../pricing.md).

## Specifics of non-replicated SSD storage {#network-nrd-storage-features}

{% include [nrd-storage-details](../../_includes/mdb/nrd-storage-details.md) %}

## Choice of storage type during cluster creation {#storage-type-selection}

The number of hosts with the _Data node_ role that can be created together with a {{ ES }} cluster depends on the selected type of storage:

* With local SSD (`local-ssd`) or non-replicated SSD (`network-ssd-nonreplicated`) storage, you can create a cluster with three or more hosts (to ensure fault tolerance, a minimum of three hosts is necessary).
* With `network-hdd` or `network-ssd` storage, you can add any number of hosts within the [current quota](./limits.md).

For more information about limits on the number of hosts per cluster, see [{#T}](./limits.md).

{% else %}

{{ mes-name }} lets you use local storage for database clusters. Local disks are physically located in the database host servers.

When creating a cluster, you can choose between the following storage types:

* Local SSD storage (`local-ssd`): The fastest disks. This storage capacity is between 10 and 2048 GB.
* Standard local disk storage (`local-hdd`): Uses slower but larger disks. Available only for hosts powered by Ice Lake or Cascade Lake processors with at least eight vCPUs.

{% endif %}
