Пример:
```
 ya make && ./prepare_tasks \
  --git_hash_x c88e6c41fb93b51d0c15153c37a9252665cfa765 \
  --git_hash_y 719e037ccebb021b897ff7ec88aa2c3feacb157b \
  --tvm_abc_mapping ~/work/tmp/PASSP-33360/tvm_abc_mapping.txt \
  --abc_managers ~/work/tmp/PASSP-33360/abc_managers.txt \
  --networks ~/work/tmp/PASSP-33360/PASSPADMIN-7286.txt \
  --oauth_token $(cat ~/work/tmp/PASSP-33360/oauth.token) \
  --out_grants ~/work/tmp/PASSP-33360/out_grants \
  --out_abc ~/work/tmp/PASSP-33360/out_abc
```

Хэши надо брать [здесь](https://github.yandex-team.ru/passport/blackbox-by-client-grants/commits/master/grants/consumer_grants.production.json)
