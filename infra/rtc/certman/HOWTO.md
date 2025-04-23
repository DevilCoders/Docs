# Certman HOWTO

## How to release new version

To prevent unapproved releases and disposable packages flood (anyone can commit
to arcadia) automatic builds for `yandex-rtc-certman` package are disabled.

Release should be manually initiated via
[CI](https://a.yandex-team.ru/projects/hostmanager/ci/releases/timeline?dir=infra%2Frtc%2Fcertman&id=rtc).

## How to deploy to RTC

Certman is deployed using standard hostctl based deploy procedure, it's
unit stored in [hostman core repo](https://bb.yandex-team.ru/projects/RTCSALT/repos/core/browse/units.d/yandex-rtc-certman.yaml).

## How to build package for manual testing

`ya package --debian --checkout --not-sign-debian pkg/pkg.json`

## Feedback

Feel free to [create a ticket](https://st.yandex-team.ru/createTicket?type=1&priority=2&tags=certman&queue=HOSTMAN)
if you spotted a bug or have a feature request.
