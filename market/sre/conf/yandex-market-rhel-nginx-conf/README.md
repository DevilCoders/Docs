==Удаленная сборка и выкладка пакета:
Собрать и выложить пакет можно в Sandbox, для этого надо запустить релизную машину yandex-market-rhel-nginx-conf:
https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/yandex-market-rhel-nginx-conf

==Локальная сборка пакета RHEL:
1. Собрать пакет через yapackage(требуется локальный rpmbuild) 
`
ya package --rpm rpmpkg.json
`
2. В результате будет собран tar архив с пакетами внутри. Распаковать его можно так:
`
tar -xvf yandex-market-rhel-nginx-conf.0.7.tar.gz
`
Посмотреть содержимое:
`
tar -tvf yandex-market-rhel-nginx-conf.0.7.tar.gz
drwxr-xr-x 0/0               0 1970-01-01 03:00 noarch/
-rw-r--r-- 0/0           22866 1970-01-01 03:00 noarch/yandex-market-rhel-nginx-conf-0.7-8517790.noarch.rpm
`
3. Собранный пакет залить в ssh://paysys-rhel.dist.yandex.net/repo/market-rhel/incoming/7:
`
scp noarch/yandex-market-rhel-nginx-conf-0.7-8517790.noarch.rpm ssh://paysys-rhel.dist.yandex.net/repo/market-rhel/incoming/7/
`
4. Заиндексировать пакет:
`
ssh paysys-rhel.dist.yandex.net sudo /usr/sbin/rpm-install -n market-rhel -v 7 
`
Если выкладывается обновленный вариант пакета с той же версией, нужно добавить ключ -f

*Для локальной сборки должен стоять на машине rpmbuild(deb пакет: rpm)
apt-get install rpm

