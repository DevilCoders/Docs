###Build tag and push docker

`docker build -t registry.yandex.net/mobilemail/reminder .`

`docker tag registry.yandex.net/mobilemail/reminder registry.yandex.net/mobilemail/reminder`

`docker push registry.yandex.net/mobilemail/reminder`

`docker pull registry.yandex.net/mobilemail/reminder`

`docker run -d registry.yandex.net/mobilemail/reminder` - run in background

`docker run --name=reminder --restart=always --env OAUTH_TOKEN_STARTREK='AQAD-***' --env OAUTH_TOKEN_TESTPALM='AQAD-***' -d registry.yandex.net/mobilemail/reminder`

`docker exec -it <container_id> bash` - open bash in running container

При необходимости работы в QYP
включить IPv6 в докере

```
cat > /etc/docker/daemon.json <<-EOF
{
    "iptables": false,
    "ip-forward": false,
    "ipv6": true,
    "dns": [
        "2a02:6b8:0:3400::1023",
        "2a02:6b8:0:3400::5005"
    ],
    "fixed-cidr": "",
    "fixed-cidr-v6": "fd00::/8"
}
EOF

service docker stop
ip link del docker0
service docker start

ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sysctl -w net.ipv6.conf.all.forwarding=1
```