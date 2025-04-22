J2 -- микро-сервис для доставки/управления сущностей в контейнеры. В настоящий момент поддерживаются:
* секреты tls-secret так как они определяются в YAV (три версии, привязанные к секрету и ротируемые каждые N часов, где N=48). Они используются для ssl session resumption тем самым оптимизируя используемый cpu на нодах, разумеется, в ущерб privacy.
* мониторинг ocsp ответов (как их закешировал cdn) и как их отдаёт ocsp Польских Товарищей [3]

Описание j2 находится тут [1], тикеты, по которым проводились работы, - [2], [3]


* ocsp check command line
          (1) проверить ocsp ответы для доменов из конфига относительно
              localhost где запущен ocsp

              [~] /usr/bin/j2 monitor run --juggler j2-ocsp-responses --debug

* ssl certificatesx expiration and serial
  number check?

           (1) проверить ssl certificates via ssl call with SNI against
               localhost

              [~] /usr/bin/j2 monitor run --juggler j2-ssl-certificates --debug

* YAV+SSL certificates logics and commands. j2 could push certificates for classes
  cdn+cache, cdn+proxy, cdn+static, ... and types cdn+static -> (1.1) static+ecc
  (1.2) static+rsa (2.1) maps+ecc, (2.2) maps+rsa.

* generating certificates - could be done via crt.yandex-team.ru. After
    we have a certificate and a key placed in one file, e.g. crls.yandex.ru.ecc.pem
    including PRIVATE KEY and CERTIFICATE. We assume that we have already new
    version of such file of corresponding cypher: ecc or rsa.

* все управляемые сертификаты имеют конфигурацию в j2 вида:

   ...
    "cdn+static":

       # each mgmt certificate has yav secret of some
       # structure, cypher and common-names to validate
       # some sanity checks
       "cdn+static+maps+ecc":
          enabled: true
          yav-secret: "sec-01en8qhgk8qay9fax1gd5nkpnb"
          destination:
            type: "cert+key"
            file: "/etc/nginx/certs/maps.yandex.net.ecc.pem"
          cipher: "ECDSA"
          common-names: [ "*.maps.yandex.net" ]

* инсталляция новых версий сертификатов в YAV
       # обновление сертификата в YAV - установка, добавление новой версии
       # class, sub-class и cipher оределяется из контента, указанные в конфиге
       # common names и cipher используются для sanity checks

       [~] j2 mgmt certificates yav set --debug --dry-run \
            --class="cdn+static" --sub-class="cdn+static+yastat+ecc" \
            --file="maps.yandex.net.ecc.crt.pem"

* listing (last versions) certificates from YAV storage
       # получение сертификатов указанных классов из j2.yaml, 
       # получаются последние версии сертификатов (они же и должны
       # быть актуальными

       [~] j2 mgmt certificates yav list --debug

* обновление конкретного класса и sub-класса сертификата
       # проверка на sanity-checks: типы сертификатов из YAV
       # и на файловой системе должны совпадать.

       [~] j2 mgmt certificates file update --class="cdn+static" \
               --sub-class="cdn+static+maps" --debug --dry-run

* еще один сигнал мониторинга - что в YAV есть более новая версия
    сертификата, отличная от инсталлированной и более новая в смысле
    NotAfter/Delta

       # проверяет набор сертификатов в YAV и на файловой системе,
       # только сообщает что что-то не так либо в YAV либо на файловой
       # системе, см bootstrap
       [~] /usr/bin/j2 monitor run --juggler \
		j2-yav-certificates --debug

* автоматическая остановка bootstrap'а web сервера контейнера если
    сертификаты не обновлены из YAV и есть сигнал что обновлять нужно 
    и NotAfter/Delta < 4h (3) есть whitelist где это работает, например,
    в локациях в которых часто хосты могут оставаться без связи или 
    их возврат к работе может затянутся на месяцы.

        # проверяем состояние подсистем: (1) delta сертификатов (2) ..
        # если не ОК и локация находится в whitelist -> выключем
        # nginx, что ещё делаем?

        [~] /usr/bin/j2 mgmt bootstrap --debug --dry-run

        [~] /usr/bin/j2 monitor run --juggler \
                j2-bootstrap --debug
     
* автоматическое обновление сертификатов из YAV по сгенерированному
    расписанию: (1) обновления только с 11:00 до 16:00 в рабочее
    время (2) каждая локация в свой timeframe (3) есть whitlist
    начинаем с простых локаций

        # запускаем "расписание" вручную "сейчас"
        [~] /usr/bin/j2 mgmt schedule --debug \
		--dry-run --now

        [~] /usr/bin/j2 monitor run --juggler \
                j2-schedule --debug

 
* STEP1: добавляем новую версию сертификата в crt формате (или сразу
    все версии, лучше делать по классам):

        # уточняем для каждого сертификата его class и subclass
        [~] /usr/bin/j2 mgmt certificates yav set --debug \
                --class="cdn+static" --sub-class="cdn+static+yastat+ecc"
                --file="./yastat.net.ecc.pem.new"

* STEP2: смотрим знает ли теперь j2 что нужно обновлять сертификаты:

        # делаем на всех нодах, все ноды независимо обновляются 
        # видим что наш сертификат выпал с такой диагностикой
        [~] /usr/bin/j2 monitor run --juggler j2-yav-certificates --debug
   
        # 0]/[6] 'cdn+static+yastat+ecc':'cipher:['ECDSA']:OK,serial:
        # ['0e:12:db:a6:63:19:f0:54:a1:31:fa:62:a8:9f:32:3b']:OK,dns-names:[...]:OK,
        # md5:[yav:'d56ad0785cce858044bef068d7c54d52' vs
        # file:'e88eb34ca48fce6c50fd5ac9f895f099']:CRIT

* делаем update по раписанию "сейчас":
   
         # для верности сначала запускаем с --dry-run, затем без
         [~] /usr/bin/j2 mgmt schedule --debug [--dry-run] --now

* смотрим опять всё ли ок в "j2-yav-certificates", ему нужна 1 минута
    чтобы проапдейтить статусы:

        [~] /usr/bin/j2 monitor run --juggler j2-yav-certificates
        [~] monrun -r yav-certificates

* дополнительная команда хозяйке на заметку (как обновить конкретный
    сертификат на целевом контейнере:

        # запускаем сначала с [--dry-run], затем без:
        [~] j2 mgmt certificates file update --debug [--dry-run] \
                --class="cdn+static" --sub-class="cdn+static+yastat+ecc"

* проверяем нужно ли CRL обновлять
        [~] j2 mgmt crl --debug --dry-run

[1] https://wiki.yandex-team.ru/tt/j2
[2] https://st.yandex-team.ru/TRAFFIC-9923
[3] https://st.yandex-team.ru/TRAFFIC-10627
[4] https://github.com/carlmjohnson/certinfo/blob/master/main.go
