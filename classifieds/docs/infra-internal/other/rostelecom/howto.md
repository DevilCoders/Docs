## Содержание
[Подключение к управлению инфраструктурой ВЦОД и выбор датацентра](#VCOD)
[Создание и удаление виртуальных серверов](#createvm)
[Подключение к консоли виртуального сервера](#connect)
[Настройка виртуального сервера](#configure)
[Как добавить/удалить сервер в текущие конфигурации](#add-del)

## Подключение к управлению инфраструктурой ВЦОД и выбор датацентра<a name="VCOD"></a>
1. Заходим в панель управления заказом ( [ссылка](https://www.cloud.rt.ru/client/orders/153565) )
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2020.49.17.png">


2. Доступы к инфраструктуре (ссылка на вход, логин и пароль) указаны на вкладке "доступ" в разделе "Виртуальные ресурсы".
Переходим по ссылке "vCloud Director" и вводим логин и пароль.

3. Выбираем нужный датацентр.
В первом датацентре (vdc_153565_service) можно настроить EDGE маршрутизатор и всё что касается сети. Во втором (vdc_153565_standard) - можно создать виртуальные сервера и получить к ним доступ.
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2020.57.08.png">

## Создание и удаление виртуальных серверов<a name="createvm"></a>
1. Подключаемся ко второму датацентру (vdc_153565_standard) и слева выбираем "Compute->Virtual Machines"
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2021.03.32.png">

2. Удаление VM.
   Для удаления VM сначала её останавливаем (Power OFF), затем удаляем (Delete) используя меню слева от названия сервера
   <img src ="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2021.07.05.png">


3. Создание VM
    1. Нажимаем на "New VM"
    2. Заполняем поля "Name", "Computer Name" и выбираем каким образом надо создать сервер: с установочного образа диска или из темплейта (я создавал из темплейта):
    <img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2021.19.49.png">
    3. Нажимаем OK и ждем создания сервера.
    4. После того как сервер создался, выбираем его из списка доступных серверов (если он запущен - останавливаем) и меняем параметры:
    - "Virtual CPUs" - указываем нужное количество ядер
    - "Memory" - количество оперативной памяти
    - "Hard Disks" - размер диска.
    - "Nics" - сетевые интерфейсы

    В сетевых интерфейсах добавляем два интерфейса с типом "VMXNET3". Для первого интерфейса указываем сеть "vertisnet" (выдаются серые IPv4 адреса), для второго - "ip_v6" (выдаются IPv6 адреса). В "IP Mode" указываем "Static - IP Pool".
    IP и MAC появятся после запуска виртуального сервера.

    <img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2021.36.00.png">


## Подключение к консоли виртуального сервера<a name="connect"></a>
1. Пароль для пользователя root.
    - Если пароль для пользователя root не менялся, то взять его можно во вкладке "Guest OS Customization"
  <img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2021.58.12.png">
    - Если сервер уже был настроен с помощью ansible плейбуки, то пароль можно взять [в секретнице](https://yav.yandex-team.ru/secret/sec-01fjcyrapgbwnp72p2yhy597qs/explore/versions).

2. Подключение с помощью Web консоли.
Выбираем "Launch Web Console" в меню управления сервером.
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-10%20%D0%B2%2022.05.35.png">

3. Подключение по ssh.
Данный метод подходит если уже есть рабочий IPsec канал с EDGE маршрутизатором.
    - Заходим по ssh на сервер с рабочим IPSec каналом ( сервер из группы [%vertis_vprod_rt_proxy](https://c.yandex-team.ru/groups/vertis_vprod_rt_proxy)).
    - Заходим по ssh на нужный виртуальный сервер под пользователем root: `ssh root@<ipv4_addr>`.

    Если сервер еще не был настроен, то потребуется ввести пароль. Если настройка сервера уже производилась, то доступ будет по ssh ключу. Список публичных ssh ключей для можно посмотреть [тут](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/rostelecom-vm-proxy/files/root/.ssh/authorized_keys)


## Настройка виртуального сервера<a name="configure"></a>
1. Настраиваем ssh
Для работы ansible (и удобного логина по ssh) в ssh конфиге описываем jump host (сервер в нашем датацентре с работающим IPSec каналом):
```
:~$ cat ~/.ssh/config

Host 192.168.0.*
  User root
  ProxyCommand ssh rt-proxy-01-vla.prod.vertis.yandex.net -W %h:%
```

2. Настраиваем окружение на виртуальном сервере
- Заходим на удаленный сервер по ssh
- Копируем свой публичный ssh ключ в ``~/.ssh/authorized_keys``
- Правим resolv.conf для использования IPv6 резолверов, пример:
```
echo '
# yandex-dns: https://dns.yandex.ru/advanced/

nameserver 2a02:6b8::feed:0ff
nameserver 2a02:6b8:0:1::feed:0ff
nameserver 77.88.8.8
nameserver 8.8.8.8' > /etc/resolv.conf
```
- Настраиваем apt на работу по IPv6
```
echo "Acquire::ForceIPv6 "true";" > /etc/apt/apt.conf.d/99force-ipv6
```

- устанавливаем ansible
```
apt-get update
apt-get install ansible
```

3. Запускаем [плейбуку](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/rostelecom-vm-proxy.yml) на локальной машинке
```
ansible-playbook rostelecom-vm-proxy.yml
```

## Как добавить/удалить сервер в текущие конфигурации<a name="add-del"></a>

1. Добавляем в ansible роль для конфигурирования виртуальных серверов
```
https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/rostelecom-vm-proxy.yml?rev=r9321782#L12
```
2. Добавляем новый хост в vars-ы для конфигурации серверов в нашем датацентре
```
https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/rt-proxy/vars/main.yml#L6
```
3. Не забываем прогонять ansible с новыми значениями
Для переконфигурирования серверов в нашем датацентре:
```
ansible-playbook vertis_vprod_rt_proxy.yml
```
