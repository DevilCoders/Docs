# crowdtesting-proxy
Yandex uses its internal network where all our internal services and testing stands work. It is called Yandex Internal Network. Our staff has an access for Yandex Internal Network by connecting to office Wi-Fi or LAN.

Usually we have two kind of security gateways:
  * Firewall, which blocks requests at network level. If you don't have an access, you'll see page loading timeout. Rules can be managed via [Puncher](https://puncher.yandex-team.ru/).
  * ACL, which blocks requests at service level. If you don't have an access, you'll see some error page (403, for instance). Rules can be managed via [IDM](https://idm.yandex-team.ru/).

Staff and outstaff must connect via VPN from outside Yandex office to get access for our internal services.
![ACL](docs/images/acl.png)

Crowdtesting proxy is a specific nginx proxy which makes it possible to allow external users from external network to have access for our internal services and resources.

Crowdtesting proxy uses an external balancer which are opened for everyone but it uses an additional permission check via webauth.

Here is how it works.
![Crowdtesting](docs/images/crowdtesting.png)

If an user opens crowdtesting proxy at the first time, he or she will see the OAuth dialog.
![Webauth](docs/images/webauth.png)

After `Allow` click Webauth checks authorization for `yandex-team.ru` domain. It means that the user must be registered at [our staff](https://staff.yandex-team.ru/).

See details at [wiki from our security team](https://wiki.yandex-team.ru/security/for/managers/kak-pustit-vneshnix-asessorov-v-svoju-testovuju-sredu).

**Note.** We don't use common crowdtest balancers. We user our own balancer, domains, and certificate to have more control and flexability. For each proxy all domains from `Available domains` list are created.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-crowdtesting-proxy |
| Qloud | https://platform.yandex-team.ru/projects/maps/front-crowdtesting-proxy |
| Certificate | [crowdtest](https://crt.yandex-team.ru/certificates/1262783?serial_number=2E2A52BA4A0219DB9E8CAEA2BE1807D2) |

## Available domains
 * `*.crowdtest.maps.yandex-team.ru`
 * `*.crowdtest.maps.yandex.az`
 * `*.crowdtest.maps.yandex.by`
 * `*.crowdtest.maps.yandex.co.il`
 * `*.crowdtest.maps.yandex.com.am`
 * `*.crowdtest.maps.yandex.com.ge`
 * `*.crowdtest.maps.yandex.com.tr`
 * `*.crowdtest.maps.yandex.com`
 * `*.crowdtest.maps.yandex.ee`
 * `*.crowdtest.maps.yandex.eu`
 * `*.crowdtest.maps.yandex.fi`
 * `*.crowdtest.maps.yandex.fr`
 * `*.crowdtest.maps.yandex.kg`
 * `*.crowdtest.maps.yandex.kz`
 * `*.crowdtest.maps.yandex.lt`
 * `*.crowdtest.maps.yandex.lv`
 * `*.crowdtest.maps.yandex.md`
 * `*.crowdtest.maps.yandex.net`
 * `*.crowdtest.maps.yandex.pl`
 * `*.crowdtest.maps.yandex.ru`
 * `*.crowdtest.maps.yandex.tj`
 * `*.crowdtest.maps.yandex.tm`
 * `*.crowdtest.maps.yandex.ua`
 * `*.crowdtest.maps.yandex.uz`

## How to add a new proxy
Create ticket from [template](https://st.yandex-team.ru/createTicket?template=4178&queue=MAPSINFRA) ([edit template](https://st.yandex-team.ru/settings/templates/issues?name=%D0%9D%D0%BE%D0%B2%D0%BE%D0%B5%20%D0%BF%D1%80%D0%BE%D0%BA%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%B2%20crowdtesting-proxy&owner=1120000000000420&queue=MAPSINFRA)). If you don't know answers for all questions, just keep then unspecified.
