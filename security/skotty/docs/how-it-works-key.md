# How it works: формат сертификатов

Т.к. у нас есть как x509 так и SSH сертификаты, то есть и два формата оных :)

{% note info %}

У пары x509 и SSH сертификатов всегда совпадают серийные номера, это сделано умышленно.

{% endnote %}

## x509

Для примера, давайте посмотрим на один из таких сертификатов:

```
$ openssl x509 -in secure.pem -text -noout
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number: 1627803124706334737 (0x16971e5144645811)
        Signature Algorithm: ecdsa-with-SHA256
        Issuer: C = RU, ST = Moscow, L = Moscow, O = Yandex, OU = Infra, CN = Skotty SSH CA (Secure)
        Validity
            Not Before: Aug  1 07:32:04 2021 GMT
            Not After : Oct 30 07:32:04 2021 GMT
        Subject: C = RU, ST = Moscow, L = Moscow, O = Yandex, OU = Infra, CN = buglloc@secure, 1.3.6.1.4.1.31337.2.1 = y15715313, 1.3.6.1.4.1.31337.2.2 = 1a767daa-f0e0-4e8e-80fd-cd897033446b, 1.3.6.1.4.1.31337.2.3 = buglloc
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (256 bit)
                pub:
                    04:09:84:78:29:75:0b:f3:85:72:55:6a:ff:5e:26:
                    ac:f9:d6:08:8d:58:56:8f:58:76:32:5a:79:9b:69:
                    89:f7:84:03:5d:15:fb:76:3a:cc:62:f4:29:7d:79:
                    06:4f:94:48:0c:b6:d6:40:53:cb:b9:72:e6:c3:c3:
                    40:0b:12:45:60
                ASN1 OID: prime256v1
                NIST CURVE: P-256
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature, Certificate Sign
            X509v3 Extended Key Usage: 
                TLS Web Client Authentication
            X509v3 Authority Key Identifier: 
                keyid:09:6F:EA:27:8D:82:41:A8:D8:7D:0F:66:AE:6D:F2:48:C6:5A:5C:4E

    Signature Algorithm: ecdsa-with-SHA256
         30:45:02:21:00:dc:73:0b:4c:f2:6b:e2:15:9f:da:18:c6:71:
         0b:73:8c:2b:70:66:6d:ec:b0:f7:e9:19:80:8e:17:9c:03:4d:
         5d:02:20:3b:51:f9:65:da:40:cf:51:33:dc:3c:b7:98:c8:26:
         45:c3:32:65:3e:10:d4:73:9e:6f:a2:09:95:51:72:04:2b
```

Каждый x509 сертификат, который выписывает Skotty, имеет:
  - уникальный серийный номер
  - Issuer соответствующий типу ключа. Т.е. проверив на каком CA выписан сертификат можно чётко понимать какие политики хранения потребовал Skotty при его выписывании
  - несколько полезных дополнительных имен:
    * OID `1.3.6.1.4.1.31337.2.1` - yubikey id
    * OID `1.3.6.1.4.1.31337.2.2` - enroll id
    * OID `1.3.6.1.4.1.31337.2.3` - логин пользователя, для которого выписывался сертификат

Т.е. в любой момент времени по сертификату можно оффлайново узнать не только назначение этого сертификата, но и кем, когда и, главное, на каком yubikey он был выписан.

## SSH

Аналогично и для SSH сертификата:

```
$ ssh-keygen -L -f ~/.skotty/pubs/ssh_yubikey_secure-cert.pub 
/home/buglloc/.skotty/pubs/ssh_yubikey_secure-cert.pub:
        Type: ecdsa-sha2-nistp256-cert-v01@openssh.com user certificate
        Public key: ECDSA-CERT SHA256:vD9aA487bZfpbmjJe3LoEJPugszFk+T4fy1ovXoqgXw
        Signing CA: ECDSA SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms (using ecdsa-sha2-nistp256)
        Key ID: "skotty:secure:buglloc:y15715313:1a767daa-f0e0-4e8e-80fd-cd897033446b"
        Serial: 1627803124706334737
        Valid: from 2021-08-01T10:32:04 to 2021-10-30T10:32:04
        Principals: 
                buglloc
        Critical Options: (none)
        Extensions: 
                permit-X11-forwarding
                permit-agent-forwarding
                permit-port-forwarding
                permit-pty
                permit-user-rc
```

Благодаря тому, что:
  - `Key ID` имеет формат `skotty:<тип>:<пользователь>:<yubikey id>:<enroll id>`
  - сервер OpenSSH должен всегда писать его в auth лог

Мы всегда можем оффлайново, только на основе лога, узнать не только назначение сертификата, его владельца и пр., но и на каком yubikey и когда он был выписан.
Например:
```
Aug  5 21:33:05 buglloc-tmp sshd[468313]: Postponed publickey for buglloc from 2a02:6b8:b081:8921::1:0 port 42590 ssh2 [preauth]
Aug  5 21:33:05 buglloc-tmp sshd[468313]: Accepted certificate ID "skotty:insecure:buglloc:sa780baa7351c7621f7bb160f9085a0fc:aca3e603-0614-4784-81d9-9e44170308e7" (serial 1628169750111859250) signed by ECDSA CA SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA via /etc/ssh/users/buglloc
Aug  5 21:33:05 buglloc-tmp sshd[468313]: Accepted publickey for buglloc from 2a02:6b8:b081:8921::1:0 port 42590 ssh2: ECDSA-CERT ID skotty:insecure:buglloc:sa780baa7351c7621f7bb160f9085a0fc:aca3e603-0614-4784-81d9-9e44170308e7 (serial 1628169750111859250) CA ECDSA SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
Aug  5 21:33:05 buglloc-tmp sshd[468313]: pam_unix(sshd:session): session opened for user buglloc by (uid=0)
Aug  5 21:33:05 buglloc-tmp systemd-logind[1264]: New session 28187 of user buglloc.
```