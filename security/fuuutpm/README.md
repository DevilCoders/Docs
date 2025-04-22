Тупой враппер над pkcs11 провайдером, который позволяет централизованно сохранять userpin.
Пример конфига:
```
$ cat /etc/fuuu-tpm.yaml
debug: true
backend: /usr/lib64/pkcs11/libtpm2_pkcs11.so.0.0.0
saved_tokens:
  -
    label: ftoken
    userpin: userpin456
```
