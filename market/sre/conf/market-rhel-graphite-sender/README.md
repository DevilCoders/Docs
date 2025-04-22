**Сборка rpm пакета /arc/trunk/arcadia/solomon/packages/yabs-graphite-sender** 
Тут лежит только спека.

**Есть пайплайн:** https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/market-rhel-graphite-sender


**Ручной метод:**

Сборка пока только руками:
ya package --rpm --key ${key} rpm.pkg.json

Выкладка:
scp "${PKG}" paysys-rhel.dist.yandex.net:/repo/market-rhel/incoming/7/

ssh paysys-rhel.dist.yandex.net sudo /usr/sbin/rpm-install -n market-rhel -v 7
