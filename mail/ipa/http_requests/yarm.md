### Создать импорт
```
curl -H 'x-real-ip:127.0.0.1' -H 'X-Request-Id:3b44a9d75a78497da3bc792f0cd90198_0c5d905ed88d4eb0a8766c9c82b2e5d3' -H 'Accept:*/*' -H 'Accept-Encoding:gzip, deflate' -H 'Host:collectors-ext-test.mail.yandex.net' -H 'User-Agent:Python/3.7 aiohttp/3.4.4' -H 'Content-Length:24' -H 'Content-Type:application/x-www-form-urlencoded' -X POST 'http://rpop-test.mail.yandex.net:3048/api/create?mdb=pg&login=rpop-test1@hmnid.ru&suid=1130000002420466&user=rpoptest3@pdd-ipa.test&server=imap.yandex.ru&port=993&ssl=1&imap=1&mark_archive_read=1&no_delete_msgs=0&json=1' --data-binary 'password=mamaamakriminal'
```

curl 'http://collectors-ext-test.mail.yandex.net/api/status?mdb=pg&popid=150001925'
curl 'http://collectors-ext-test.mail.yandex.net/api/list?mdb=pg&suid=1130000002425068'
