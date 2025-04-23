# yamail-network-scripts
Скприты настройки сети

update-network:
 - правит:
   - /etc/hosts
   - /etc/hostname
   - /etc/network/interfaces (netconfig)
   - /etc/resolv.conf

- при необходимости создает /etc/sysctl.d/99-tunnelRS.conf

- manage-balancer:
  - закрывает/открывает хост для баласнера, в том числе тунельного

- sysctl.d:
  - sysctl.d/95-disable-pmtu.conf: отключает PMTU

[Сборка в Sandbox](https://sandbox.yandex-team.ru/task/1349620602/view)
