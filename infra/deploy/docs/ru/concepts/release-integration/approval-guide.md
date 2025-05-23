# Настройка двойных апрувов в Y.Deploy

Двойные апрувы запрещают выкладку релизов и любые изменения стейджа, если они не подтверждены несколькими членами команды. Таким образом, если включить политику апрува для стейджа, то вступают в силу следующие изменения:

1. Необходимо подтверждать релизные тикеты, созданные релизной интеграцией.
1. Необходимо подтверждать любые ручные изменения стейджа.

В данном документе описана настройка двойных апрувов, а также работа со стейджами с включённой политикой апрува.

## Гайд по UI {#ui-guide}

### Создание политики апрува {#create-approval-policy}

Настройка начинается с создания политики апрува. Это можно сделать на странице релизов.

![approval-create-0-arrows.png](../../_assets/concepts/approval-create-0-arrows.png)

В выпадающем окне необходимо настроить создаваемую политику апрува.

![approval-create.png](../../_assets/concepts/approval-create.png)

* **Approval Policy** — политику апрува можно настроить, но не включать. Если политика апрува выключена, то подтверждения не нужны.
* **Regular approves** — минимальное количество пользователей, которые должны подтвердить изменения (релизный тикет или ручные правки стейджа), чтобы его можно было закоммитить. Подтверждать могут только пользователи, обладающие ролью `Regular Approver`.
* **Mandatory approves** — флаг, ужесточающий политику апрува. Если этот флаг выставлен, то, кроме всего прочего, необходимо, чтобы среди пользователей, подтвердивших изменения, был хотя бы один пользователь, обладающий специальной ролью `Mandatory Approver`.
* **Regular Approvers** и **Mandatory Approvers** — роли `Regular Approver` и `Mandatory Approver` для пользователей нужно запрашивать через `IDM`. Если в политике апрува выключен флаг `Mandatory Approve`, то подтверждать изменения могут только пользователи с ролью `Regular Approver`, пользователи с ролью `Mandatory Approver` подтверждать изменения в этом случае не смогут. Запросить соответствующие роли в IDM можно перейдя по ссылке `Manage Roles`.

### Подтверждение релизных тикетов {#approve-deploy-tickets}

Если политика апрува настроена, то после создания релизного тикета его нужно подтвердить. Без получения нужных апрувов тикет нельзя закоммитить. Подтвердить тикет можно по кнопке `Approve`.

![created-ticket-arrows.png](../../_assets/concepts/created-ticket-arrows.png)

Пока тикет не закоммичен, пользователь может снять своё подтверждение — кнопка `Disapprove`.

![approved-ticket-arrows.png](../../_assets/concepts/approved-ticket-arrows.png)

Количество полученных подтверждений и список пользователей, поставивших/снявших подтверждения, приводится в колонке `Approves`.

![approve-list.png](../../_assets/concepts/approve-list.png)

После того как необходимое количество подтверждений собрано, релизный тикет можно закоммитить. Дальнейшая работа с релизными тикетами описана в документе: [Релизная интеграция](release-integration.md#tikety).

### Ручные изменения стейджа с включённой политикой апрува {#manual-updates}

Если в стейдже включена политика апрува, то редактировать стейдж напрямую нельзя. Необходимо сначала создать и опубликовать драфт с изменениями. Рассмотрим, как это делается в UI.

1. Открываем новую форму редактирования стейджа. При включенной политике апрува редактировать стейдж из старой формы не получится.
    ![approval-stage-edit.png](../../_assets/concepts/approval-stage-edit.png)

1. Вносим необходимые изменения и нажимаем **Update**.
    ![approval-stage-edit-update.png](../../_assets/concepts/approval-stage-edit-update.png)

1. Внимательно изучаем дифф! На странице с диффом нажимаем кнопку **Save as Draft**.
    ![approval-stage-draft.png](../../_assets/concepts/approval-stage-draft.png)

В результате изменения не будут сразу же применены к стейджу. Вместо этого создастся тикет специального вида. В этом тикете хранится дифф изменений. Апрув драфт-тикета выполняется так же, как апрув тикета релизной интеграции (как описано выше).

Драфт-тикеты, как и тикеты релизной интеграции, отображаются на странице **Releases**. Чтобы отрисовать только драфт-тикеты, необходимо использовать фильтр.
![approval-stage-filter.png](../../_assets/concepts/approval-stage-filter.png)

После апрува тикет можно закомитить, и уже тогда изменения применятся к стейджу.
