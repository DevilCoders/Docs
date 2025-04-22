# Утилита для экстракции x-token'а с борта устройства и передачи его в бекенд для воскрешения

Читает токены из `/data/quasar/account_storage.dat` и передает парами в HTTP-запросе

Usage: `LD_LIBRARY_PATH=/system/vendor/quasar/lib/ ./lazarus https://somewhere.yandex.ru/some_handle`.
NB: URL should have no cgi parameters or anchors!
Building: `ya make --target-platform default-android-armv8a -r -DSTRIP -DARCADIA_CURL_DNS_RESOLVER=MULTITHREADED`.

На каждый вычитанный аккаунт будет сделан один HTTP GET запрос на заданный URL.
В запросе будет передан cgi-параметр `blob`, в котором -- JSON вида `{"x_token": "<x-token string>", "oauth_token": "<oauth token string>"}`, зашифрованный публичным ключом и закодированный в base64.

Все части ключа хранятся в https://yav.yandex-team.ru/secret/sec-01dweya1p9n9wn4m8gnf803vvp/explore/version/ver-01dweya1q7fqwhgbtn2tnmy449 , публичный зашит в код.

Расшифровать можно, например, так:
```
$ echo '123123123123==' | base64 --decode > xtoken_json.crptd
$ openssl rsautl -decrypt -oaep -in xtoken_json.crptd -out xtoken.json -inkey pkcs8.key
```

См https://st.yandex-team.ru/ALICE-5027
