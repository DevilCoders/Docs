Скрипт переноса пимем и папок ящика одного пользователя в ящик другого.
Состоит из двух подкоманд:
1.  `read-mail-box` - считывает метаинформацию о папках ящика и исходники писем заднного пользователя и сохраняет их на файловой системе в указанном каталоге. Структура каталога повторяет структуру папок ящика пользователя. В каждом каталоге сохранется метаинформация о папке и письмах в ней, а также исходники (*.eml) самих писем. Ходит в **hound** за списком папок и писем. Ходит в **mbody** за исходниками писем. Команда принимает следующие (основные) параметры:
    - `uid` - uid пользователя
    - `dir` - каталог для сохранения/загрузки дампа ящика
    - `hound-host` - хост hound-а
    - `hound-port` - порт hound-а
    - `hound-ticket` - service-ticket для похода в hound
    - `mbody-host` - хост mbody
    - `mbody-port` - порт mbody
    - `mbody-ticket` - - service-ticket для похода в mbody

2.  `write-mail-box` - считывает метаинформацию о папках и письмах исходного ящика с диска и загружает письма в целевой ящик. Ходит в **hound** за списком папок целевого ящика. С помощью **mops** создает недостающие папки в целевом ящике. Загружает письма в ящик с помощью **mxback**.
Команда принимает следующие (основные) параметры:
    - `uid` - uid пользователя
    - `email` - email пользователя
    - `dir` - каталог загрузки дампа ящика
    - `hound-port` - хост hound-а
    - `hound-port` - порт hound-а
    - `hound-ticket` - service-ticket для похода в hound
    - `mops-host` - хост mops-а
    - `mops-port` - порт mops-а
    - `mops-ticket` - service-ticket для похода в mops
    - `mxback-host` - хост mxback-а
    - `mxback-port` - порт mxback-а
    - `mxback-ticket` - service-ticket для похода в mxback


```bash
#!/bin/bash

SRC_UID="320175938"

SRC_OUTPUT_DIR="/tmp/zoonew2"

SRC_HOUND_HOST="meta.mail.yandex.net"
SRC_HOUND_PORT="443"
SRC_HOUND_SERVICE_TICKET="3:serv:CLFmEPjW3fYFI...ujyaJnGFg"

SRC_MBODY_HOST="mbody.mail.yandex.net"
SRC_MBODY_PORT="80"
SRC_MBODY_SERVICE_TICKET="3:serv:CLFmEMLX3fYFI...vIFw15kUQ"

DST_UID="4044081257"
DST_EMAIL="yndx.zoonew2.test2@yandex.ru"

DST_INPUT_DIR="${SRC_OUTPUT_DIR}-copy"

DST_HOUND_HOST="meta-test.mail.yandex.net"
DST_HOUND_PORT="443"
DST_HOUND_SERVICE_TICKET="3:serv:CLFmEIPk3fYFI...voL4aUZug"

DST_MOPS_HOST="mops-test.mail.yandex.net"
DST_MOPS_PORT="80"
DST_MOPS_SERVICE_TICKET="3:serv:CLFmEM7k3fYFI...ykqQX2zPg"

DST_MXBACK_HOST="mxback-test.mail.yandex.net"
DST_MXBACK_PORT="2443"
#DST_MXBACK_SERVICE_TICKET=""

COPY_BOX_BIN=`dirname $0`/copy-box


${COPY_BOX_BIN} read-mail-box \
	--uid=${SRC_UID} \
	--dir=${SRC_OUTPUT_DIR} \
	--hound-host=${SRC_HOUND_HOST} \
	--hound-port=${SRC_HOUND_PORT} \
	--hound-ticket=${SRC_HOUND_SERVICE_TICKET} \
	--mbody-host=${SRC_MBODY_HOST} \
	--mbody-port=${SRC_MBODY_PORT} \
	--mbody-ticket=${SRC_MBODY_SERVICE_TICKET}

cp -R ${SRC_OUTPUT_DIR}/ ${DST_INPUT_DIR}/

${COPY_BOX_BIN} write-mail-box \
	--uid=${DST_UID} \
	--email=${DST_EMAIL} \
	--dir=${DST_INPUT_DIR} \
	--remove-saved \
	--hound-host=${DST_HOUND_HOST} \
	--hound-port=${DST_HOUND_PORT} \
	--hound-ticket=${DST_HOUND_SERVICE_TICKET} \
	--mops-host=${DST_MOPS_HOST} \
	--mops-port=${DST_MOPS_PORT} \
	--mops-ticket=${DST_MOPS_SERVICE_TICKET} \
	--mxback-host=${DST_MXBACK_HOST} \
	--mxback-port=${DST_MXBACK_PORT}
```
