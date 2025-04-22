This repository contains debianization of yandex-taximeter-dotnet package.

Build:
debuild --no-lintian --check-dirname-level 0 --no-tgz-check -b

Upload:
dupload --to yandex-taxi-common --nomail yandex-taximeter-dotnet_1.0.0-yandex0_amd64.changes
