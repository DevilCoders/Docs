# DismissEmployee
This script for purging employees from YandexClassifieds organization.  
Ticket nubmer: [**VERTISADMIN-18086**](https://st.yandex-team.ru/VERTISADMIN-18086)  
The script do actions which described [here](https://wiki.yandex-team.ru/vertis-admin/checklists/firing/)  
**Build Example:**  
```sh
$ go build
```  
**Usage Example:**
```sh
$ ./dismiss_employee employeeStaffName
```



### Requires
* [**lxc-mngr.sh**](https://github.com/YandexClassifieds/admin-utils/blob/master/lxc-mngr.sh). To delete lxc containers. 
* [**qyp-mngr.sh**](https://github.com/YandexClassifieds/admin-utils/blob/master/qyp-mngr.sh). To delete qyp containers.
* [**dns-monkey.pl**](https://wiki.yandex-team.ru/dynamic-dns/dns-monkey-roadmap/).
* **$ADDITIONAL_SCRIPTS_PATH** evn varialbe. This variable should contains path to dns-monkey.pl and lxc-mngr.sh separated by :
```sh
$ cat $ADDITIONAL_SCRIPTS_PATH 
/usr/bin/dns-monkey.pl:/home/jazkamer/work/admin-utils/lxc-mngr.sh:/home/jazkamer/work/admin-utils/qyp-mngr.sh
```
* **$GITHUB_TOKEN** evn varialbe. Github OAuth token should have scope repo.  
     You can get token [here](https://github.com/settings/tokens)
* **$CONDUCTOR_OAUTH_TOKEN** evn variable.  
More info [here](https://juggler.yandex-team.ru)
* Your **staffLogin** should be [here](https://github.com/YandexClassifieds/DismissEmployee/blob/master/tools/auth.go)
