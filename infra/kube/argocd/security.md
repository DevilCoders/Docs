# Multi-cloud infra

## Скоуп задач, которые мы хотим решать

* Развертывание в Yandex.Cloud, в AWS, в Azure облачных ресурсов таких как базы данных, кластера Kubernetes, etc
* Выкладки приложений в Kubernetes
* Предоставление инструментов для настройки CI/CD процессов

## Обзорная схема

![overview](assets/overview.png)

## Шаг 1

На первой итерации целимся в настройку релизных процессов приложений.

1. Пуш docker образов в публичные registry. Хранение кода, запуск тестов, сборка образов остается внутри яндекса (
   sandbox, arcadia)

   С помощью YA_PACKAGE или аналогичной таски образ будет собираться в sandbox, после этого пушиться в registry в
   YC/AWS/Azure.

2. Хранение deploy конфигов (спеки кубера) в git репозитории

   В GitLab/GitHub/BitBucket репозитории будут храниться конфиги Kubernetes (Deployment, Service).

   На первое время это будет репозиторий в Managed GitLab в Yandex.Cloud.

3. Актуализация target state приложения в соответствии с deploy конфигами.

   ArgoCD синкает спеки из git репозитория и применяет их в Kubernetes.

   В git аутентифицируется по deploy token для GitLab или аналогам в других системах. В Kubernetes аутентифицируется
   через kubeconfig.

   Имея доступ к git можно управлять ресурсами, которыми управляет ArgoCD (vanilla Kubernetes, crossplane)

## Шаг 2

1. Управление ресурсами платформы через crossplane

   Crossplane от имени IAM user'а управляет облачными ресурсами (RDS, S3, etc). Права на IAM User можно ограничивать с
   помощью Policy.

   Доступ к crossplane ограничивается на уровне Kubernetes RBAC.

3. Управление секретами

   [Vault + external-secrets-operator](../examples/vault/README.md)

4. Настройка CI/CD вне инфры яндекса.

   Воркеры CI запущены в инфраструктурной инсталяции Kubernetes как `kind: Job`.

   Единого выбора GitLab CI / TeamCity / etc пока нет.

