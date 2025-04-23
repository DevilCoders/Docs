Сборник полезных и не очень скриптов
- yaki - ya make + хитрые ключики
- perstvm - ленивый (не по принципу работы, а по жизни) генератор tvm токенов для ручной отладки ручек, закрытых tvm
- persec - обновление секретов в няне
- persidea - удобные параметры для ya ide idea

Для того, чтобы perstvm работал, нужно [получить роль](https://wiki.yandex-team.ru/passport/tvm2/getabcrole/) 'TVM ssh пользователь' в [marketpers](https://abc.yandex-team.ru/services/marketpers/)

```
# linux
sudo ln -s /home/$USER/arc/arcadia/market/pers/common/src/main/bin/yaki.sh /usr/bin/yaki
sudo ln -s /home/$USER/arc/arcadia/market/pers/common/src/main/bin/perstvm.sh /usr/bin/perstvm
sudo ln -s /home/$USER/arc/arcadia/market/pers/common/src/main/bin/persec.sh /usr/bin/persec
sudo ln -s /home/$USER/arc/arcadia/market/pers/common/src/main/bin/peridea.sh /usr/bin/peridea

# macos
ln -s $ARCADIA_ROOT/market/pers/common/src/main/bin/yaki.sh /usr/local/bin/yaki
ln -s $ARCADIA_ROOT/market/pers/common/src/main/bin/perstvm.sh /usr/local/bin/perstvm
ln -s $ARCADIA_ROOT/market/pers/common/src/main/bin/persec.sh /usr/local/bin/persec
ln -s $ARCADIA_ROOT/market/pers/common/src/main/bin/persidea.sh /usr/local/bin/persidea
```
