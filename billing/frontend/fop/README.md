# What is it?
Balance FOP for print forms

# How to add offer
Add new offer to the (login as "robot-balance-wiki"):
https://wiki.yandex-team.ru/balance/printdocuments/offers/
Run build:
https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_BalanceFop_Offers

# View data (test):
https://user-balance.greed-tm.paysys.yandex.ru/invoice-for-output.xml?object_id={INVOICE_ID}&rep_type=invoice

# View data (prod):
```python
import xml.etree.ElementTree as et
from balance import multilang_support
from balance.publisher import fetch

# scp -r greed-tm1h.paysys.yandex.net:/var/www/xs5/balance-tanker .
multilang_support.set_trans_dir({PATH_TO_TANKER_XML})

i = fetch.get_data_for_publisher({SESSION_PROD}, {INVOICE_ID}, None, 'invoice')
t = et.ElementTree(i)

t.write({OUTPUT_PATH}, encoding='utf-8')
```

# Java server:
https://github.yandex-team.ru/Billing/balance-fop-server

# Robot tests:
https://github.yandex-team.ru/Billing/balance-tests/blob/master/balance/pagediff_tests/test_paystep.py

# Technical specification
https://wiki.yandex-team.ru/balance/tz/killpublisher/

# Debian package
```yandex-balance-fop```

# Apache FOP
https://xmlgraphics.apache.org/fop/
https://xmlgraphics.apache.org/fop/1.0/knownissues_overview.html

# Разработка
При разработке используется статика развернутого локально репозитория `tools`.
- задать `TOOLS_DIR`, пример:
```$bash
export TOOLS_DIR=~/work/tools
```
- запустить генерацию ПФ:  

Если нужна для счета, указав название XML-файла счета из папки `test/fixtures/invoice` без расширения. Пример:
```$bash
./dev-invoice.sh invoice.isr.yandex-go.650
```
Если нужна для акта, указав название XML-файла акта из папки `test/fixtures/act` без расширения. Пример:
```$bash
./dev-act.sh act.sw_ur.service_7.personal_account.EUR.firm_7
```

# Просмотр логов
- выполнить установку по [инструкции](https://a.yandex-team.ru/arc/trunk/arcadia/billing/library/tools/baf).
- запустить `baf log` (среда testing)

# Обработка изображений
Если в результирующем документе изображения масштабируются некорректно, нужно настроить resolution в Photoshop.
Image -> Resize -> Image Size

# CLI example
```bash
# With pipe:
cat fop/invoice_by.xml | fop -c fop/fop.xconf -xml - -xsl print_form.xsl -pdf -

# With xml file:
fop -c fop/fop.xconf -xml invoice_by.xml -xsl print_form.xsl -pdf result.pdf
fop -c fop/fop.xconf -xml invoice_tr.xml -xsl print_form.xsl -rtf result.rtf

# Dev:
TANKER_PATH=$(pwd)/tests/tanker \
make -C fop-resources/xsl/i18n clean all

FOP_ENV=local \
FOP_COMMAND=$(pwd)/fop-2.1/fop \
FOP_RESOURCES=$(pwd)/fop-resources \
python bfop/fop.py ./tests/fixture/invoice/invoice.sw_ur.usd.14.xml > out.pdf
```

# Python example
```python
from tests.bfop import fop

xsl_path = 'PATH_TO_XSL_FILE'
xml_data = '<root>...</root>'

print fop.render(xml_data, xsl_path, fop.OutputFormat.RTF)
```

# Test
```bash
TANKER_PATH=$(pwd)/tests/tanker \
make -C fop-resources/xsl/i18n clean all

FOP_ENV=local \
FOP_COMMAND=$(pwd)/fop-2.1/fop \
FOP_RESOURCES=$(pwd)/fop-resources \
python -m pytest -k test_fop_pdf_invoice
```

# Deploy

Requires ```openjdk-7-jre-headless``` package to be installed. Creates ```/usr/bin/fop``` symlink
to the installed FOP distribution

# How to add Java cert

See: https://wiki.yandex-team.ru/security/ssl/sslclientfix/

If you need to specify ```JAVA_HOME``` for Mac OS you can use:
```bash
JAVA_HOME=$(/usr/libexec/java_home -v 1.8)
```

```bash
wget https://crls.yandex.net/YandexInternalRootCA.crt -O .
sudo $JAVA_HOME/bin/keytool -importcert -file ./YandexInternalRootCA.crt -keystore $JAVA_HOME/jre/lib/security/cacerts  -alias "Yandex"

# Default key store password: changeit
```

## Сборка yb-fop-cli
В текущую сборку пакет `yb-fop-cli` не включен ввиду крайне редкой необходимости его обновления. Но если потребуется его собрать, это нужно сделать руками на одной из сборочных машин. 

Команды могут быть примерно такими:
```(bash)
debuild --no-lintian --no-tgz-check -I -b -k83722C67
dupload ../*.changes
```

В папке `debian` файлы `*.old` на время сборки должны быть без суффикса. 