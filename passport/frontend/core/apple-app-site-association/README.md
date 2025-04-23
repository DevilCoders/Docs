# apple-app-site-association
apple-app-site-association.json

Чтобы не искать каждый раз как подписывать:

```(sh)
cat apple-app-site-association.json | \
   openssl smime -sign \
   -inkey passport.yandex.ru.key \
   -signer passport.yandex.ru.crt \
   -certfile passport.yandex.ru.intermediate \
   -noattr -nodetach \
   -outform DER > apple-app-site-association
```
