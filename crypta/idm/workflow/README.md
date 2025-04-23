Конгфигурация в коде для https://idm.yandex-team.ru/system/crypta/workflow

Автоматически обновится в IDM после коммита этим Action: [код](https://a.yandex-team.ru/arc_vcs/crypta/idm/workflow/a.yaml?rev=efba1723ad0fcf0a2471ad7f9fd0b737735251fd#L14), [CI](https://a.yandex-team.ru/projects/cryptaall/ci/actions/launches?dir=crypta%2Fidm%2Fworkflow&id=crypta-idm-workflow-release). Апдейты аутентифицируются с помощью oauth-токена `robot-crypta` в приложении Crypta API, в котором, в свою очередь, запрошено право "Использовать IDM" в соответствии с [документацией](https://wiki.yandex-team.ru/intranet/idm/API/public/#authentication). Также для этого `robot-crypta` является Ответственным в системе `Idm -> Крипта` в соответствии с [документацией](https://wiki.yandex-team.ru/intranet/idm/rolesdescr/#vkonkretnojjsisteme).


Если нужно обновления вручную:
```
ya make
./update_workflow --environment Production
```
В этом случае токен получится автоматически на основе имени пользователя в системе, нужно быть Ответственным в `Idm -> Крипта`.
