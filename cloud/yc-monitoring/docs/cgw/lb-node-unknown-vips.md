# lb-node-unknown-vips

**Значение**: на lb-node приехало правило, для которого она на знает, как анонсировать (или как снимать анонс) vip'а. Эта проверка, фактически, подможество https://wiki.yandex-team.ru/cloud/devel/loadbalancing/monitorings/#lb-node-announces , но берёт инфу из Solomon, а не с хоста.
**Воздействие**: не будем принимать пользовательский тарфик или, наоборот, принимать и отправлять в /dev/null
**Что делать**: на lb-node можно узнать, какой vip проблемный:
`curl 0x0:4050/debug/gobgp`
Дальше будут два списка: not announced vips - vip'ы, для которые не знаем, как анонсировать и not withdrawn - vip'ы, которые не знаем, как удалять. Список известных сетей можно посмотреть в секции gobgp.announces:
`sudo cat /etc/yc/loadbalancer-node/config.yaml`
если CIDR'а для vip'а действительно нет, то нужно понять, откуда он появился. Возможно, дёрнуть duty tool info по vip'у и найти логи в API, откуда он взялся. Если это валидный сценарий, то узнать в /duty vpc-api актуальный список fip bucket'ов и сверить с конфигом lb-node. Если там не хватает, то добавить нужные fip bucket'ы в surveyor.
