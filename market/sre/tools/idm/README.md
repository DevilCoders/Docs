# IDM REST API Client
> A primitive REST API client for https://idm.yandex-team.ru

## Usage example

A easy way to try is using REPL

```
> ya make --checkout repl
> repl/idm-repl
>>> helpme()
IDM REPL r3249342

It helps you work with IDM.

>>> c = idm.IdmClient(get_token())

>>> r = idm.RoleRequestGenCfg(group_id=41953, gencfg_group='IVA_MARKET_PROD_GENERAL', root=True)

>>> result = c.post_role_request(r)

>>> print(result['human_state'])
```

To find group_id use Staff-API, e.g. a staff group https://staff-api.yandex-team.ru/v3/groups?url=yandex_mnt_fin_market or an ABC service https://staff-api.yandex-team.ru/v3/groups?url=svc_market_report

## Links

https://wiki.yandex-team.ru/intranet/idm/API/public/
