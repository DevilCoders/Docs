# AWACS_EXTERNAL_CERTIFICATES

Awacs namespace must have "Yandex CA" certificate.

## Reason
It is needed to be able to use your balancer via secured HTTPS connection.

{% note info %}

See more documentation on https://wiki.yandex-team.ru/awacs/certs/

{% endnote %}

## Solution
1) Go to the your awacs namespace.
2) Go to the certificates list through "Show Certificates" button in 'Certificates' section.
3) Add new certificate by "Order Certificate" button.

---
_[Source](https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/guidelines/src/tests/awacs/certificates.test.ts#L25-41)_
