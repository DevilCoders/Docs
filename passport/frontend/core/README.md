```
NODE_OPTIONS="--max_old_space_size=4096" make
npm config set yandex-passport-frontend:port NNNN
make start
```

Теперь можно перейти на https://NNNN.passportdev.yandex.ru/profile/ или https://NNNN.passportdev2.yandex.ru/profile/, в зависимости от того, на каком мы деве
