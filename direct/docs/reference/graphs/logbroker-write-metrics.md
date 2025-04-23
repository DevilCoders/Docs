# Метрики записи в Logbroker

На этой страничке приведены метрики записи данных нами в логброкер — для оценки общей утилизации квоты и распределения скорости записи по топикам.
Графики сгруппированы по паре: кластер logbroker — наш аккаунт.

Кластера:
- **lbkx** — геораспределенный production кластер Logbroker
- **lbkxt** — геораспределенный prestable кластер Logbroker
- **lbk** — однодатацентровый production кластер Logbroker
- **lbkp** — однодатацентровый prestable кластер Logbroker


## lbkx — direct (prod) { #lbkx-direct }
Production Директа: экспорты, ESS.

### QuotaConsumed { #lbkx-direct-write-quota }
Процент использования квоты на запись.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&service=quoter_service&resource=write-quota&sensor=QuotaConsumed|Limit&cluster=lbkx&host=cluster&quoter=/Root/PersQueue/System/Quoters/direct&graph=direct-logbroker-write-quota-usage&graphOnly=y'></iframe>

### BytesWrittenOriginal { #lbkx-direct-write-bytes }
Объём записи по топикам.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&OriginDC=cluster&Topic=%21total&Account=direct&graph=auto&hideNoData=true&graphOnly=y'></iframe>


## lbk — direct (prod) { #lbk-direct }
Production Директа: обычные логи (вроде ppclog_cmd, messages).

### QuotaConsumed { #lbk-direct-write-quota }
Процент использования квоты на запись по ДЦ.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&service=quoter_service&resource=write-quota&sensor=QuotaConsumed%7CLimit&cluster=lbk&host=Iva%7CMan%7CMyt%7CSas%7CVla&quoter=%2FRoot%2FPersQueue%2FSystem%2FQuoters%2Fdirect&graph=direct-logbroker-write-quota-usage&hideNoData=true&graphOnly=y'></iframe>

### BytesWrittenOriginal { #lbk-direct-write-bytes }
Графики объёма записи по топикам для каждого ДЦ.

#### IVA { #lbk-direct-write-bytes-iva }

<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&Topic=%21total&Account=direct&OriginDC=Iva&graph=auto&hideNoData=true&graphOnly=y'></iframe>

#### SAS { #lbk-direct-write-bytes-sas }

<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&Topic=%21total&Account=direct&OriginDC=Sas&graph=auto&hideNoData=true&graphOnly=y'></iframe>

#### VLA { #lbk-direct-write-bytes-vla }

<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&Topic=%21total&Account=direct&OriginDC=Vla&graph=auto&hideNoData=true&graphOnly=y'></iframe>


## lbkx — direct-np (testing) { #lbkx-direct-np }
Тестовые и разработческие окружения Директа: экспорты, ESS.

### QuotaConsumed { #lbkx-direct-np-write-quota }
Процент использования квоты на запись.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&service=quoter_service&resource=write-quota&sensor=QuotaConsumed|Limit&cluster=lbkx&host=cluster&quoter=/Root/PersQueue/System/Quoters/direct-np&graph=direct-logbroker-write-quota-usage&graphOnly=y'></iframe>

### BytesWrittenOriginal { #lbkx-direct-np-write-bytes }
Объём записи по топикам.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkx&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&OriginDC=cluster&Topic=%21total&Account=direct-np&graph=auto&hideNoData=true&graphOnly=y'></iframe>


## lbkxt — direct (testing) { #lbkxt-direct }
Тестовые и экспериментальные экспорты Директа.

### QuotaConsumed { #lbkxt-direct-write-quota }
Процент использования квоты на запись.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&service=quoter_service&resource=write-quota&sensor=QuotaConsumed|Limit&cluster=lbkxt&host=cluster&quoter=/Root/PersQueue/System/Quoters/direct&graph=direct-logbroker-write-quota-usage&graphOnly=y'></iframe>

### BytesWrittenOriginal { #lbkxt-direct-write-bytes }
Объём записи по топикам.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkxt&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&OriginDC=cluster&Topic=%21total&Account=direct&graph=auto&hideNoData=true&graphOnly=y'></iframe>


## lbk — direct-np { #lbk-direct-np }
_В момент составления этой страницы на графиках были одни нули, поэтому пока их пропускаем._


## lbkp — direct-test (testing) { #lbkp-direct-test }
Обычные логи с тестовых и разработческих окружений Директа.

### QuotaConsumed { #lbkp-direct-test-write-quota }
Процент использования квоты на запись по ДЦ.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&service=quoter_service&resource=write-quota&sensor=QuotaConsumed%7CLimit&cluster=lbkp&host=Iva%7CMan%7CMyt%7CSas%7CVla&quoter=%2FRoot%2FPersQueue%2FSystem%2FQuoters%2Fdirect-test&graph=direct-logbroker-write-quota-usage&hideNoData=true&graphOnly=y'></iframe>

### BytesWrittenOriginal { #lbkp-direct-test-write-bytes }
Графики объёма записи по топикам для каждого ДЦ.

#### MYT { #lbkp-direct-test-write-bytes-myt }
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkp&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&Topic=%21total&l.Account=direct-test&graph=auto&l.OriginDC=Myt&hideNoData=true&graphOnly=y'></iframe>


## lbkp — direct (testing) { #lbkp-direct }
Непродакшн Директа.

### QuotaConsumed { #lbkp-direct-write-quota }
Процент использования квоты на запись по ДЦ.
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=direct&service=quoter_service&resource=write-quota&sensor=QuotaConsumed%7CLimit&cluster=lbkp&host=Iva%7CMan%7CMyt%7CSas%7CVla&quoter=%2FRoot%2FPersQueue%2FSystem%2FQuoters%2Fdirect&graph=direct-logbroker-write-quota-usage&hideNoData=true&graphOnly=y'></iframe>

### BytesWrittenOriginal { #lbkp-direct-write-bytes }
Графики объёма записи по топикам для каждого ДЦ.

#### MYT { #lbkp-direct-write-bytes-myt }
<iframe height='400' width='100%' markdown="1" frameBorder="0"
src='https://solomon.yandex-team.ru/?project=kikimr&cluster=lbkp&service=pqproxy_writeSession&host=cluster&sensor=BytesWrittenOriginal&Topic=%21total&l.Account=direct&graph=auto&l.OriginDC=Myt&hideNoData=true&graphOnly=y'></iframe>
