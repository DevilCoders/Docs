# Как выдать права IAM пользователям на provider-aws ресурсы

* Запросить роль в ABC: любую роль в [SDC external clouds](https://abc.yandex-team.ru/services/sdc_external_clouds) или
  DevOps роль в [Crossplane RTC](https://abc.yandex-team.ru/services/crossplane_rtc/)

  После этого шага для доменного пользователя создастся IAM user с ролью view.

* Выдать права на управление ресурсами provider-aws

    * Добавляем нового пользователя в [sdg-sandbox](./sdg-sandbox.yaml) в секцию `subjects`

      В качестве `name` берем iam id пользователя
      из [Users and roles](https://console.cloud.yandex.ru/iam?section=users)

    * Коммитим в аркадию, чтобы не потерять изменения
    * Применяем изменения (Права на создание есть у [sdg-sandbox.rolebinding.admin](./sdg-sandbox-rbac.yaml))

      ```shell
      kubectl --context crossplane apply -f infra/kube/aws/rbac/sdg-sandbox.yaml
      ```


