# How it works: KRL

Т.к. мы больше не таскаем публичные SSH ключи пользователей, а полагаемся на CA - CA нужно каким-то образом мочь отозвать ранее выписанный сертификат. Например, в случае инцидента безопасности. Для этого в OpenSSH есть поддержка [KRL (Key Revocation List)](https://raw.githubusercontent.com/openssh/openssh-portable/master/PROTOCOL.krl). Если кратенько, то это просто файл бинарного формата, который содержит:
  - серийные номера/ключи/key id/etc сертификатов, которым не стоит верить
  - подписи списка на ключах CA

Если говорить о нашей реализации, то:
  - серверная часть генерирует KRL раз в час, исключая сертификаты отозванные менее получаса назад
  - в KRL попадают только `secure` + `insecure` + `sudo` сертификаты, этими же CA KRL подписывается
  - KRL доступен по адресу: `https://skotty.sec.yandex-team.ru/api/v1/ca/krl/all.zst`
  - в заголовке `ETag` всегда должен быть `md5` от содержимого

### Пример KRL

```
# Обратите внимание на ETag
% http https://skotty.sec.yandex-team.ru/api/v1/ca/krl/all.zst
HTTP/1.1 200 OK
Accept-Ranges: bytes
Access-Control-Allow-Origin: *
Content-Length: 1344
Content-Type: application/krl+zst
Date: Thu, 05 Aug 2021 18:14:18 GMT
Etag: "1289c870996c62aa9d756725202ce9d7"
Last-Modified: Thu, 05 Aug 2021 18:00:00 GMT
X-Amz-Request-Id: a851c0391fff7f95
X-Amz-Version-Id: 0005C8D3B003E2D8



+-----------------------------------------+
| NOTE: binary data not shown in terminal |
+-----------------------------------------+

# Скачиваем KRL
% http https://skotty.sec.yandex-team.ru/api/v1/ca/krl/all.zst > all.zst

# Проверяем целостность
% md5sum all.zst 
1289c870996c62aa9d756725202ce9d7  all.zst

# Распаковываем
% zstd -d all.zst 
all.zst             : 2152 bytes

# Парсим
% krltool parse all 
parse file:  all
signed by:
  -  SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
  -  SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
  -  SHA256:3c8D5PtFgdPqUjrVmy8n1MDl2fbgt6ON6NdRzu8VGow
sections:
  - [0] KRL_SECTION_CERTIFICATES:
    * CA: SHA256:9iugZLu67ykk8KutH/wJPudHxT4PismFrfy9ehLXOms
        + [0] KRL_SECTION_CERT_SERIAL_LIST:
           1626730073832989346
           1627026844070302593
           1627027174999685203
  - [1] KRL_SECTION_CERTIFICATES:
    * CA: SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
        + [0] KRL_SECTION_CERT_SERIAL_LIST:
           1626730073883643508
           1627026844029669294
           1627027174966476923
  - [2] KRL_SECTION_CERTIFICATES:
    * CA: SHA256:3c8D5PtFgdPqUjrVmy8n1MDl2fbgt6ON6NdRzu8VGow
        + [0] KRL_SECTION_CERT_SERIAL_LIST:
           1626730073914213284
           1627026843988521781
           1627027174925988390
```

Из примера выше видно, что все выглядит как и ожидалось:
  - есть заголовок `ETag` с `md5` от содержимого
  - KRL подписана всеми нужными CA
  - KRL содержит отозванные сертификаты на всех трех CA

P.S. К сожалению, хорошего парсера KRL не нашлось, поэтому написали свой [krltool](https://a.yandex-team.ru/arc_vcs/security/skotty/krltool).

### Как обновить KRL на сервере

Важно заметить, что с обновлением KRL нужно быть осторожным, т.к. в случае его порчи или отсутствия можно заблокировать доступ на сервер всем пользователям. Выдержка из [sshd_conf](https://man.archlinux.org/man/sshd_config.5.en#RevokedKeys):
> Note that if this file is not readable, then public key authentication will be refused for all users.

Демо плохого KRL:
```
Aug  5 20:03:42 buglloc-tmp sshd[455682]: error: Error checking authentication key RSA SHA256:C0Q14mSJLVITEyGsP6QLE1Z/GfTwEq1mLzVemnVch0E in revoked keys file /etc/ssh/revoked_keys: invalid format
```

Поэтому flow обновления должен быть максимально строг:
  - скачиваем KRL во временный файлик/память
  - проверяем, что `md5` сошелся
  - проверяем, что SSH может его попарсить. Проще всего сделать это с помощью `ssh-keygen`: `ssh-keygen -Qf revoked_keys`
  - опционально, проверяем что KRL подписан нужными вам CA
  - только после этого заменяем старый KRL новым

В случае проблем - ничего не обновляем, зажигаем лампочку, дебажим.

### auth.log
При попытке аутентификации с отозванным сертификатом в `auth.log` будет соответствующая запись:
```
Aug  5 19:42:01 buglloc-tmp sshd[452520]: Failed publickey for buglloc from 2a02:6b8:b081:8916::1:13 port 47904 ssh2: ECDSA-CERT ID skotty:insecure:buglloc:s604249f78f0831fd6a48c6867c868edb:56154248-319d-4eca-99b5-b2b79e2b4ea9 (serial 1627027174966476923) CA ECDSA SHA256:9PsYUcGRMBPVEHlt5gZYXduP7fCceJ7BVnoV3NsXZsA
Aug  5 19:42:01 buglloc-tmp sshd[452520]: error: Authentication key ECDSA-CERT SHA256:GKrfaiq0mDEISrUviqMSUzDoa3CWXTtq23lBJsfIAsI revoked by file /etc/ssh/revoked_keys
```