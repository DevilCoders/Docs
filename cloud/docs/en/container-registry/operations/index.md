---
title: "How to work with Docker images. Step-by-step instructions"
description: "Step-by-step instructions for working with Docker images in {{ yandex-cloud }}. From the article you will learn how to manage a Docker image, registry, repository and automatic policies. We will tell you in detail about creating, deleting, uploading and downloading Docker images."
---

# Step-by-step instructions for {{ container-registry-name }}

To work with Docker images, [authenticate in {{ container-registry-name }}](authentication.md).

{% if product == "yandex-cloud" %}

## Working with {{ coi }} {#coi}

For more information about working with a {{ coi }} image, see the documentation [{{ cos-name }}](../../cos/).

{% endif %}

## Managing a Docker image {#docker-images}

* [{#T}](docker-image/docker-image-list.md)
* [{#T}](docker-image/docker-image-create.md)
* [{#T}](docker-image/docker-image-push.md)
* [{#T}](docker-image/docker-image-pull.md)
* [{#T}](docker-image/docker-image-delete.md)

## Managing Helm charts {#helm-charts}

* [{#T}](helm-chart/helm-chart-list.md)
* [{#T}](helm-chart/helm-chart-push.md)
* [{#T}](helm-chart/helm-chart-pull.md)
* [{#T}](helm-chart/helm-chart-delete.md)

## Managing a registry {#registry}

* [{#T}](registry/registry-list.md)
* [{#T}](registry/registry-create.md)
* [{#T}](registry/registry-update.md)
* [{#T}](registry/registry-delete.md)

## Managing a repository {#repository}

* [{#T}](repository/repository-list.md)
* [{#T}](repository/repository-create.md)

## Managing Docker image lifecycle policies {#lifecycle-policy}

* [{#T}](lifecycle-policy/lifecycle-policy-list.md)
* [{#T}](lifecycle-policy/lifecycle-policy-create.md)
* [{#T}](lifecycle-policy/lifecycle-policy-update.md)
* [{#T}](lifecycle-policy/lifecycle-policy-dry-run.md)
* [{#T}](lifecycle-policy/lifecycle-policy-delete.md)

## Working with roles {#roles}

* [{#T}](roles/grant.md)
* [{#T}](roles/get-assigned-roles.md)
* [{#T}](roles/revoke.md)