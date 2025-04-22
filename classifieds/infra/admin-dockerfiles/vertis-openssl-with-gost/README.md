Готовые образы:

## registry.yandex.net/vertis/vertis-openssl-with-gost:engine-1.1.0.3
Образ с:
openssl engine
(dynamic) Dynamic engine loading support
(gost) Reference implementation of GOST engin

engine gost -c
(gost) Reference implementation of GOST engine
 [gost89, gost89-cnt, gost89-cnt-12, gost89-cbc, grasshopper-ecb, grasshopper-cbc, grasshopper-cfb, grasshopper-ofb, grasshopper-ctr, md_gost94, gost-mac, md_gost12_256, md_gost12_512, gost-mac-12, gost2001, gost-mac, gost2012_256, gost2012_512, gost-mac-12]

openssl ciphers|tr ':' '\n'|grep GOST
GOST2012-GOST8912-GOST8912
GOST2001-GOST89-GOST89

