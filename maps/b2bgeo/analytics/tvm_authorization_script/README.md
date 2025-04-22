This directory is used for generating tvm_tickets. Read more about tvm on wiki:
https://wiki.yandex-team.ru/passport/tvm2/quickstart

Many services require tvm authorization. Here's how it works:
1. Register your service ("TVM application") as "passport-type" resource in ABC. Icar resource: https://abc.yandex-team.ru/services/B2BGEO/resources/?view=consuming&layout=table&supplier=14&type=47&show-resource=25463948
2. get tvm secret (see link to yav.yandex-team.ru in ABC service). For icar it is stored in `icar.sas.yp-c.yandex.net:/home/robot-b2bgeo/.tvm_self_secret`
3. discover client_id of the service that you want to access
4. get ticket (see below)
5. use ticket in http requests. See dst service documentation. Typical way is using headers like `headers={'X-Ya-Service-Ticket': 'your ticket'}`
6. Note that ticket has limited lifetime, maximal length is 12 hours, so you need to re-generate tickets often.

To generate ticket manually you can use
```
Z_TVM_TICKET=$(cat /home/robot-b2bgeo/.tvm_self_secret | ya tool tvmknife get_service_ticket client_credentials --src 2024967 --dst 2023123 -S)
```
*here 2024967 is client_id of icar, 2023123 is client_id of go.zora.yandex.net proxy*

In this directory we use simple arcadia tvm client to generate tickets. \
Dst-services are listed in `icar_tvm_config.json` \
Tokens are usually stored in `icar:/b2bgeo/data/tvm_tickets`

When deploying to new icar:
- create `newicar:/b2bgeo/data/tvm_tickets`
- place `icar_tvm_config.json` to `newicar:/b2bgeo/data/tvm_tickets/tvm_config.json`
- or change file paths as you wish in `icar_tvm_config.json` and `__main__.py`
- ya-make binary in this directory and place it to `newicar:/b2bgeo/data/tvm_tickets`
- place tvm-secret to `/home/robot-b2bgeo/.tvm_self_secret`
- run ClusterMaster target `write_tvm_tickets`
