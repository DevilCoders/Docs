## C3PO package

Docker C3PO image for deploy.

### Pre-installation steps
[Install docker](https://docs.docker.com/engine/install/ubuntu/) and [add user to docker group](https://docs.docker.com/engine/install/linux-postinstall/).

Configure dockerd for QYP:
```
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
```

Enable IPv6 forwarding: 
`sudo sysctl -w net.ipv6.conf.all.forwarding=1`

Restart daemon & relogin into your machine.


### Build package:
`ya package package.json --docker`
