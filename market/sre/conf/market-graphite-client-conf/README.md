**Пакет, привозящий конфиги для market-graphite-sender.**

Сборка deb и раскатка через пайплайн: https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/market-graphite-client-conf


Сборка rpm и раскатка через пайплайн: https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/market-rhel-graphite-client-conf
На данный момент пакет автоматически не инсталлится в репозитории, нужно сделать  
``
ssh paysys-rhel.dist.yandex.net sudo /usr/sbin/rpm-install -n market-rhel -v 7    
``  
после сборки.

На хосты RTC везем через salt: https://bb.yandex-team.ru/projects/RTCSALT/repos/saltstack/browse/common/components/market/market-14/market-base/packages.sls#37
