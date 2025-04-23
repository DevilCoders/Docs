# yaoblako-common

Роль для раскатки v4 хостов в публичном Яндекс.Облаке, копипаста из [leaseweb-common](https://github.com/YandexClassifieds/vertis-ansible/tree/master/roles/leaseweb-common) и [leaseweb-firewall](https://github.com/YandexClassifieds/vertis-ansible/tree/master/roles/leaseweb-firewall).   
Требует `gather_facts: true`. Пример подключения:
```
 ~/ans/vertis-ansible-beeline  cat vertis_vprod_beeline_proxy.yml
- hosts: vertis_vprod_beeline_proxy
  gather_facts: yes
  become: yes
  roles:
    - yaoblako-common
```   

Для первого запуска потребуется указать пользователя и запрос пароля, например:
```
 ~/ans/vertis-ansible-beeline  apl vertis_vprod_beeline_proxy.yml -u vertis -k|tail -n4
SSH password: 
PLAY RECAP *******************************************************************************************************************************************************************************************************************************************************************************
beeline-proxy-01-central1a.prod.vertis.yandex.net : ok=11   changed=0    unreachable=0    failed=0   
beeline-proxy-01-central1b.prod.vertis.yandex.net : ok=11   changed=0    unreachable=0    failed=0   
```   

В дальнейшем можно ходить под рутом со своим ключом:
```
 ~/ans/vertis-ansible-beeline  apl vertis_vprod_beeline_proxy.yml -u root|tail -n4
PLAY RECAP *******************************************************************************************************************************************************************************************************************************************************************************
beeline-proxy-01-central1a.prod.vertis.yandex.net : ok=11   changed=0    unreachable=0    failed=0   
beeline-proxy-01-central1b.prod.vertis.yandex.net : ok=11   changed=0    unreachable=0    failed=0   
```
