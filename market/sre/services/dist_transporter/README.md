# Dist Transporter
> A MVP of service for sharing and downloading dists

## Usage
https://st.yandex-team.ru/MARKETTECH-655#5cfd25eaba1349001f611502

## Packages
Use ```ya package``` or Sandbox task YA_PACKAGE to build the following packages
- debian ```deb/pkg.json``` (use 16.04 or greater to get package with support for systemd)
- tarball for a Nanny service ```rtc/pkg.json``` (use Sandbox resource type MARKET_DIST_TRANSPORTER)
- tarball for a Report Nanny service ```rtc-report/pkg.json``` (use Sandbox resource type MARKET_DIST_TRANSPORTER)

## TODO
1. Add monitoring handler `/monitoring`
1. Add metrics, handler `/unistat` for YASM
1. Add dumping and restoring state
1. Fix TODOs in srcs

## Links
https://st.yandex-team.ru/CSADMIN-28718
https://st.yandex-team.ru/MARKETTECH-655
