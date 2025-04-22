###How to contribute (for developers)
1. Send a Pull Request.
2. Create a ticket on https://st.yandex-team.ru/VERTISADMIN.

###Build package
https://teamcity.yandex-team.ru/project.html?projectId=VertisAdmin_ConfigVsNginx&tab=projectOverview

###Workflow how to make a change and don't make a fuckup (for admins)
Follow next rules:
- Don't do any changes without ticket on https://st.yandex-team.ru/VERTISADMIN.
- Don't change master, make branch and merge it.
- Ask colleagues for review your changes before making merge. If reviewer agrees with changes they'll leave comment that contants ```:8ball:```.
- Don't rush!

###How to allow access for Yandex only if service lives behind slash
```
    real_ip_header X-Forwarded-For-Y;
    inlcude include/set_real_ip_from-ynets;
    include include/access-ynets-only;
```

###How to create branch from PR
Somtimes we need to deploy some changes only to testing. Then we create a separate branch.
```
git fetch origin pull/<PR id>/head:<new branch name>
```
