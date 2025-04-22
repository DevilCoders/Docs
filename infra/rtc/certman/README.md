# Host certificate management tool

`certctl` - command line tool for host certificates management.

`certctl` may be used to:
* Manage certificate (reissue when certificate approaching it's end of life).
* Manually issue new certificate (a way to fix host certificate when existing
  one already expired, not valid or revoked).
* Debug: there are auxiliary subcommands to dump certs, crls and so on. See
  `--help` for full list.

## Monitoring

### Juggler
Check name: `certman`.

Possible values:
  * `WARN` - certificate is valid but needs update (and update attempts fail)
    or state file is outdated (i.e. no `certctl manage` within last 24 hours)
  * `CRIT` - certificate is invalid (expired, absent, etc)

**IMPORTANT**
`certman` check is [used by wall-e](https://st.yandex-team.ru/HOSTMAN-115) as
host redeploy trigger (CRITs only: host has no chances to reissue new cert
without valid one)

### YASM
Exports metrics available in [HOSTMAN-CERT](https://yasm.yandex-team.ru/template/panel/HOSTMAN-CERT/) panel.
Metrics are:
  * `Invalid certs on hosts` - speaks for itself
  * `Needs update certs on hosts` - certificates are still valid, but need update.
  Means that we continuously fail to issue new certificate. Must be internal error or CRT API failures.

### Diagnosis
In case of alert notification SRE must manually log on into affected host and check certificate manager status:

```
$ certctl status
Valid: True
Update required: False
Days left: 13
$
```
  * If `Update required` is `True` see `/var/log/certctl.log` for details.
  Most likely we have trouble with CRT and need to contact their [administrators](https://abc.yandex-team.ru/services/certificator/).
  * If `Valid` is `False` - `message` field will contain error why exactly certificate manager assumes certificate as invalid.
  It can be expired and one should consult manual issuing section of this document.
  * Also one must check `/var/log/certctl.log` if something obscure is happening.

One can decode `/etc/certs/capi.pem` using with following command: `sudo certctl info`.
Which will load and render **first certificate** in PEM in almost human readable format.

## Logic
We have following tiers:
  * experimental
  * prestable
  * production

### Experimental

Request cert for 14 days, update if 13 or less days left.

### Prestable

Request cert for 14 days, update if 7 or less days left.

### Production
  * Requests certificate for a year.
  * Checks how many days left.
  * If `days left < 10` - try to update.
  * If `days left > 100` - do nothing.
  * If it is night - do not update.
  * If it will be weekend in a year - do not update.
  * Else if `hash(hostname) % 100 == days left` (pseudo code) - update.

Thus we spread certificate expiration dates.

## Emergency/manual issuing
В случае аварии необходимо **вручную** перевыпустить сертификат на хосте.

Есть два варианта:
  * Выпуск от имени [робота](#Роботный-пользователь-для-выпуска-сертификатов) - **рекомендуемый**. Взять [токен](https://yav.yandex-team.ru/secret/sec-01dcnzq6ef976hjqmt7tdvzy8k) из секретницы.
  * Выпуск от своего имени - **только в случае аварии**.
  Для этого с помощью `certctl gen-token` получить токен. Для перевыпуска
необходимо **иметь роль в IDM**, запросить роль можно по [ссылке](https://idm.yandex-team.ru/user/nekto0n/roles#rf=1,rf-role=1cQ7DCpy#certificator/group-4;;10;%D0%90%D0%B2%D0%B0%D1%80%D0%B8%D0%B9%D0%BD%D1%8B%D0%B9%20%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D1%8B%D0%BF%D1%83%D1%81%D0%BA%20%D1%81%D0%B5%D1%80%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82%D0%BE%D0%B2%20%D0%B2%20RTC,f-status=all,sort-by=-updated,rf-expanded=1cQ7DCpy) 

### Починка одного хоста

`ssh {HOSTNAME} sudo certctl issue --token {TOKEN}`

В случае отсутствия роли в IDM, скрипт даст ссылку на запрос роли в консоль.

### Починка множества хостов
  * Положить список хостов в файл `hosts.txt`
  ```
  ssh jmon-master.search.yandex.net
  jctl list raw -service walle_host_certificate  --status CRIT | grep "Certificate /etc/certs/capi.pem expired" | awk '{print $1}' > hosts.txt
  ```
  * Выполнить скрипт `for i in $(cat hosts.txt); do ssh $i "sudo certctl issue --token {TOKEN}"; done`

**Важно**: в случае, если проблемных хостов много, `jctl list` вернёт только первые N событий и действия нужно повторять итеративно.

### Роботный пользователь для выпуска сертификатов
  * заведён [robot-certman](http://staff.yandex-team.ru/robot-certman)
  * доступ к его [паролю](https://yav.yandex-team.ru/edit/secret/sec-01dcm2zz6fkgm7eb67e17k81jy/explore/versions) дан SRE
  * запрошена роль в IDM на перевыпуск сертификатов - [link](https://idm.yandex-team.ru/user/robot-certman/roles#f-status=all,sort-by=-updated,role=8726687)
  * сгенерирован [токен](https://yav.yandex-team.ru/secret/sec-01dcnzq6ef976hjqmt7tdvzy8k)

Токен сгенерирован [nekto0n'ом](https://staff.yandex-team.ru/nekto0n):
  * Зашёл на стафф под роботом и добавил свою публичную часть ключа роботу.
  * Запустил `certctl gen-token -u robot-certman`
  * Положил токен в секретницу, доступ дал SRE.  

## Сторонние ресурсы
- Про хостовые сертификаты: https://wiki.yandex-team.ru/iss3/security/
- Про API Центра сертификации: https://wiki.yandex-team.ru/Intranet/crt/api/

## Feedback

Feel free to [create a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=certman&queue=HOSTMAN)
if you spotted a bug or have a feature request.
