Nginx Configs Generator
===

This service generates includes with branches for NginX.  
It gives us opportunity balance 1% traffic to branch by yandexuid cookie.
More information you can find [here](https://wiki.yandex-team.ru/vertis-admin/NGINX/branches/).  

This service is supplied to hosts as debian package via ansible-pull.  
The package is used on next clusters:
- vertis_vtest_lb;
- vertis_prod_lb.

Build configuration for package you can find [here](https://t.vertis.yandex-team.ru/project/VertisAdmin_NginxConfigsGenerator?mode=builds).  
The version of package set up in [role](https://github.com/YandexClassifieds/vertis-ansible/blob/master/roles/nginx-configs-generator/tasks/main.yml#L3-L9).  
If you deployed new version you need to restart the service on hosts by hands via command: `systemctl restart nginx-configs-generator.service`  
We have a dashboard with useful metrics for this service [here](https://grafana.vertis.yandex-team.ru/d/8kMxoiiMk/nginx-configs-generator).  
Detailed logs you can see on hosts via command: `journalctl -u nginx-configs-generator`

