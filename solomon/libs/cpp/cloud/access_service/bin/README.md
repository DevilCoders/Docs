## Command Line Client

! Should be run inside Yandex internal network

Usage example:
```bash
(PRE-PROD) ivanzhukov@solomon-gateway-00:~$ ./access_service_client authenticate --host as.private-api.cloud-preprod.yandex.net --port 4286 --iam-token=.SoMeToKeN~VaLuE==HeRe

Subject: { user_account { id: "bfbmkbd3sfl46e42ijt6" } }
```

```bash
(PRE-PROD) ivanzhukov@solomon-gateway-00:~$ ./access_service_client authenticate --host as.private-api.cloud-preprod.yandex.net --port 4286 --iam-token=t1.9euenp7...

Subject: { service_account { id: "bfbiri3br828jqjnao36" folder_id: "aoee25j5t74btmr627kp" } }
```

See `--help` for more
