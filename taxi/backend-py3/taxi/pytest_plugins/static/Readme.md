This folder contains private and public key that are used in some tests.

Those keys were generated via `openssl req -x509 -sha256 -nodes -newkey rsa:4096 -days 5000 -keyout mockserver_ssl.key -out mockserver_ssl.crt` command. Write `localhost` to CN (Common Name) question to avoid problems with curl (example: https://github.com/envoyproxy/envoyproxy.github.io/issues/94)!
