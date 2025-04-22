# sign

Скрипт для генерации подписи

## Пример использования

`-kv` - список ключей и версий, уже должен лежать на диске в конфиге.

```
$ ya make
$ ./sign -kv 1 -s salt arg_to_sign_1 arg_to_sign_2 arg_to_sign_3
Signing ['arg_to_sign_1', 'arg_to_sign_2', 'arg_to_sign_3'] with key version '1' and salt 'salt'
salt:1:oLAeDNqXeS7bkFksmIzzTbJxPZ8DuW+iDRG9hcQM8Ys=
```
