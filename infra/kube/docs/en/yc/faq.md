## Frequently asked questions

Здесь сформулированы наиболее часто задаваемые вопросы и ответы на них. В случае если Вы не нашли ответ
на какой-то вопрос или имеющийся ответ не совсем понятен, или Вы не уверены, что все понимаете правильно,
то обращайтесь к kaganovich1@yandex-team.ru

1. What is YC roles? How to get them?

YC roles are granted by request from ABC service. For each YC role informational security
department approved corresponding IAM roles in Yandex.Cloud. Mapping between YC roles and IAM roles
 is accessible by link: [mapping](https://wiki.yandex-team.ru/yc4y-t/abc-to-iam-role-mapping/)

2. What is Yandex organization? What clouds are inside it? How to move in Yandex organization?

At the end of 2021 Yandex.CLoud introduced a notion of organization as a one level above clouds.
It is impossible to create new clouds without organization and exising clouds shall be
moved into Yandex organization.

In correspondence with [plans](https://clubs.at.yandex-team.ru/cloud/2217), Yandex organization
shall include all clouds related to Yandex services. Move will be produced
in unified manner and separately for every cloud.

The main feature of Yandex organization is a unified federation which contains
only Yandex employees. Therefore, in case cloud has its own federation,
all customized federation users will be mapped to unified federation users.
Cloud access after migration is by [URL](https://console.cloud.yandex.ru/federations/bpf301hnejf1t12ndk5m).

3. Why users in Yandex organization can't have admin role?

There exists rules for Yandex.Cloud and approved by informational security department
 [cloud rules](https://wiki.yandex-team.ru/security/policies/yandex-cloud-rules).
admin role allows to assign roles in cloud. It's unsafe and leads to uncontrolled
manual role assignment. In order to prevent it, admin roles is not assigned.
More details by [link](https://wiki.yandex-team.ru/security/policies/yandex-cloud-rules/#avtorizacijavjandeksoblakeiamroli)

4. How to create service account and assign roles to it?

There exist 2 ways: make it manually or delegate it to support team

4.1 Manual creation

For manual service account creation it is necessary to request YC Administrator role
and provide information about purpose of request.
Informational security department approves temporal role assignment.
YC Administrator role corresponds to IAM роль editor which allows to create service account
but doesn't aloow to assign roles.

For role assignment it is necessary to use roles synchronization functionality.

4.2 Delege creation by analogy with [ticket](https://st.yandex-team.ru/CLOUDSUPPORT-128911)
and wait for ticket execution.

5. How to create folder in cloud?

In order ti create folder in cloud it is necessary to request YC Administrator role and provide the
purpose for the role.
Informational security department approves temporal role.
YC Administrator role corresponds to IAM role editor which allows to create folder.

6. Roles synchronization directory has many yaml files. Which file is used for
   Yandex organization?

File prod-yandex.yaml has synchronization rules for Yandex organization.

7. Do standard yaml block exist that has YC roles to IAM roles mapping?

Yes, the file is accessible by  [link](https://wiki.yandex-team.ru/yc4y-t/yandex-team-federation/).








