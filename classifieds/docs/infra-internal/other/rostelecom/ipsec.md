IPSec каналы установлены между виртуальным маршрутизатором (EDGE) ВЦОД РТК и нашими серверами в группе [%vertis_vprod_rt_proxy](https://c.yandex-team.ru/groups/vertis_vprod_rt_proxy). Отдельный канал для каждого нашего сервера.

## Настройка IPSec в ВЦОД

1. Подключаемся в первому датацентру (vdc_153565_service).
2. Слева выбираем "Networking -> Edges" и выбираем наш EDGE маршрутизатор (Edge-153565).
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-11%20%D0%B2%2015.45.43.png">
3. Переходим в Services.
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-11%20%D0%B2%2015.47.52.png">
4. Текущую статистику подключений можно посмотреть во вкладке "Statistics", в подменю: "IPsec VPN".
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-11%20%D0%B2%2015.49.05.png">
5. Для настройки/создания/удаления соединений заходим в "VPN" -> "IPsec VPN" -> "IPsec VPN Sites".
6. Выбираем текущее соединение или нажимаем на "+" для добавления нового.
<img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-11%20%D0%B2%2015.55.09.png">
7. Настраиваем соединение
    - Enabled: `true`
    - Name: имя соединения (желательно назвать по короткому имени сервера с которым планируется созать канал)
    - Local Id: `2a01:620:b:4::4004"` (IPv6 адрес EDGE маршрутизатора)
    - Local Endpoint: `2a01:620:b:4::4004"` (IPv6 адрес EDGE маршрутизатора)
    - Local Subnets: `192.168.0.0/24` (серая IPv4 сеть виртуальных серверов в ВЦОД)
    - Peer Id: `<IPv6>` (IPv6 адрес сервера с которым устанавливаем соединение)
    - Peer Endpoint: `<IPv6>` (IPv6 адрес сервера с которым устанавливаем соединение)
    - Peer Subnets: <IPv4/32> (серый IPv4 адрес сервера с которым устанавливаем соединение)
    - Encryption Algorithm: `AES256`
    - Authentication: `PSK`
    - Pre-Shared Key: `XXXXX` (указываем секретный ключ, текущий лежит в [секретнице](https://yav.yandex-team.ru/secret/sec-01fhzk2gfppgpyhp6r7wzfmn3a/explore/versions))
    - Diffie-Hellman Group: `DH5`
    - Digest Algorithm: `SHA-256`
    - IKE Option: `IKEv2`
    - IKE Responder Only: `true`
    - Session Type: `Policy Based Session`
    - Нажимаем "keep" для сохренения.
    Пример конфигурации
    <img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-11%20%D0%B2%2016.05.01.png">
    <img src="https://jing.yandex-team.ru/files/kasev/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202021-11-11%20%D0%B2%2016.06.39.png">


## Настройка IPSec на серверах в нашем ДЦ.
- Для установки IPSec соединений используем ПО: strongswan
- Конфиг IPSec соединения привозится в файл `/etc/ipsec.conf` из темплейта в ansible роли rt-proxy ( [ссылка на темплейт](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/rt-proxy/templates/etc/ipsec.conf.j2) )
- Пример конфигурации и описание ключевых полей
    ```
    # ipsec.conf - strongSwan IPsec configuration file
    config setup
    charondebug="all"
    uniqueids=yes

	# strictcrlpolicy=yes
	# uniqueids = no

    # Sample VPN connections
    conn rt-ipsec
        type=tunnel
        auto=start
        keyexchange=ikev2
        authby=secret
        left=2a02:6b8:c02:505:8000:4098:a571:d847 # IPv6 адрес сервера
        leftsubnet=192.168.1.1/32                 # IPv4 адрес севера
        right=2a01:620:b:4::4004                  # IPv6 адрес EGDE
        rightsubnet=192.168.0.0/24                # IPv4 подсеть с виртуальными серверами в ВЦОД
        ike=aes256-sha256-modp1536!
        esp=aes256-sha256!
        aggressive=no
        keyingtries=%forever
        ikelifetime=28800s
        lifetime=3600s
        dpddelay=30s
        dpdtimeout=150s
        dpdaction=restart
    ```
- PSK секрет привозится в файл `/etc/ipsec.secrets` ansible темплейтом ([ссылка](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/rt-proxy/templates/etc/ipsec.secrets.j2)).
##  Полезные команды для работы с IPSec
- Посмотреть статус IPSec
`ipsec status`
- Посмотреть расширенный статус IPSec
`ipsec statusall`
- Перезапустить IPSec
`service strongswan restart`
