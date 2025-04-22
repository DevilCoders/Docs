Ideas:
- https://webthesis.biblio.polito.it/8475/1/tesi.pdf
- http://publications.csail.mit.edu/lcs/pubs/pdf/MIT-LCS-TM-637.pdf
- https://core.ac.uk/download/pdf/327178651.pdf
- https://sebymiano.github.io/publication/2018-fulvio-toward/2018-fulvio-toward.pdf
- https://webthesis.biblio.polito.it/15302/1/tesi.pdf
- file:///Users/esafronov/Downloads/sustainability-12-03068.pdf
- http://www.sysnet.ucsd.edu/sysnet/miscpapers/p2-baboescu.pdf
- http://klamath.stanford.edu/~pankaj/thesis/chapter4.pdf
- http://cseweb.ucsd.edu/~susingh/papers/hyp-sigcomm03.pdf
- file:///Users/esafronov/Downloads/ERFC_An_Enhanced_Recursive_Flow_Classification_Alg.pdf
- https://d-nb.info/993170161/34
- file:///Users/esafronov/Downloads/diss.pdf
- https://engineering.purdue.edu/~vijay/papers/2010/efficuts.pdf
- http://www.diva-portal.org/smash/get/diva2:1249035/FULLTEXT01.pdf
- http://ccr.sigcomm.org/online/files/p207.pdf
- HiCuts, HyperCuts
- https://github.com/blockchain-research-foundation/AVX-Memmove/blob/master/memcmp.c
- YANET

## Исходные данные

Рулсет состоит из нескольких десятков тысяч правил (на данный момент около 40'000 только HBF правил) в ipfw формате 
вида:

```
# Правило с обычными сетями.
allow tcp from 2a02:06b8:1234::/48 to any 443

# Правило с wildcard-сетями.
allow tcp from 2a02:06b8:0:0:0:1234::/ffff:ffff:0:0:ffff:ffff:: to any 443

# Правило с хостнеймом.
add allow tcp from { vizator.yandex.ru } to { _NOCMGMTSRV_ } 80

# Правило с макросами, которые раскрываются в список сетей или хостнеймов.
add allow tcp from { _NOCSRVNETS_ } to { _NOCMGMTSRV_ } 80,443

# Порт ренджи и протоколы могут варьироваться.
add allow udp from { _ROUTERSNETS_ } to { _NOCMGMTSRV_ } 21,69,80,1024-65535

# Встречаются также правила, в которых в качества src/dst перечислено сразу несколько (иногда довольно много)
# макросов, сетей или хостнеймов.
add allow tcp from { _GENCFG_MSK_MYT_TRAVEL_ADMIN_PROD_ or _GENCFG_MSK_MYT_TRAVEL_BACKEND_PROD_ or _GENCFG_MSK_MYT_TRAVEL_WIZARD_PROD_ or _GENCFG_SAS_TRAVEL_ADMIN_PROD_ or _GENCFG_SAS_TRAVEL_BACKEND_PROD_ or _GENCFG_SAS_TRAVEL_INDEXER_PROD_ or _GENCFG_SAS_TRAVEL_WIZARD_PROD_ or _SEARCHMETANETS_ or _GENCFG_TRAVEL_PROD_NETS_ } to { _VERTISPROD_ } 2181,9042,36400,36420,36432,36445
...

# Финальное правило, которое запрещает все, что не разрешено.
deny ip from any to any
```

### Стадии
- Парсинг ipfw правил
- Парсинг макросов и DNS кэша
- Построение LPM
- Построение структур для портов, флагов, протокола
- Деклассификация.

## Учения
## Трансляция в ebpf

#### Wildcard IPv6 lookup

## Трансляция в iptables

### Поиск правил
- __builtin_ffs
- https://webthesis.biblio.polito.it/15302/1/tesi.pdf
- https://sebymiano.github.io/publication/2018-fulvio-toward/2018-fulvio-toward.pdf
- https://core.ac.uk/download/pdf/327178651.pdf
- http://pages.cs.wisc.edu/~akella/CS740/S07/740-Papers/BV01.pdf

- http://www.sysnet.ucsd.edu/sysnet/miscpapers/p2-baboescu.pdf
- http://klamath.stanford.edu/~pankaj/thesis/chapter4.pdf

## Обновление правил

MUST BE ATOMIC(!)

