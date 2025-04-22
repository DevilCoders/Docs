# Wireguard setup 


For example: 
* vpc net 192.168.1.0/24
* wg net 192.168.69.0/24

We need start wg server on one host from vpc.
This host must have public IP address.
eg.
* Public IP 20.187.40.219
* Private IP 192.168.69.5 from vpc

### Start wg server on this host:

* Install wg on host
```
sudo add-apt-repository ppa:wireguard/wireguard
sudo apt install wireguard
```
* Enable IP Forward 
```
/etc/sysctl.conf

net.ipv4.ip_forward = 1
```
enable with `sysctl -p`
* Generate server and client configs with `wg genkey | sudo tee client_private.key | wg pubkey | sudo tee client_public.key`
* Write wg server config in `/etc/wireguard/wg0.conf`
```
[Interface]
PrivateKey = <wg-server private key>
Address = 192.168.69.1/24
ListenPort = 51820
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
PublicKey=<client private key>
AllowedIPs=192.168.69.2/24
PersistentKeepalive=25
```
* `systemctl start wg-quick@wg0` # start wg server
* `systemctl enable wg-quick@wg0` # enable onboot start

### Setup client:

* Install wireguard on dev host
* Write client config in `/etc/wireguard/wg0.conf` on dev host
```
[Interface]
PrivateKey = <client private key>
Address=192.168.69.2/24 # Client IP address, **static?**

[Peer]
 PublicKey=<server public key>
 Endpoint=20.187.40.219:51820 # Public IP of wg server
 AllowedIPs = 192.168.0.0/16 # Forward all traffic to server for (192.168.1.0/24 VPC) and (192.168.69.0/24 WG net)
```
* Start client with `wg-quick up wg0` or `systemctl start wg-quick@wg0`
* Check 
```
# IP from Wg net 
ping 192.168.69.1

# IP from vpc
ping 192.168.1.5 # VPC address from wg server
ping 192.168.1.4 # Other host from VPC

traceroute 192.168.1.4 # Traffic routing through 192.168.1.5 to 192.168.1.4
```





