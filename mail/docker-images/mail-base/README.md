# Базовый почтовый докер-образ

На каждый пулл-реквест запускается сборка с пушем в registry тега `pr-XXX-N` (`XXX` — номер PR, `N` — номер сборки).

На каждый мердж в транк [запускается релизный флоу](https://a.yandex-team.ru/projects/sre_vteam/ci/releases/timeline?dir=mail%2Fdocker-images%2Fmail-base&id=mail-base-release) c пушем тега `latest` и `rNNN` (`NNN` — номер ревизии).

Тег последней сборки можно взять отсюда:

<img src="https://jing.yandex-team.ru/files/avanes/2022-07-15T07:48:41Z.046f538.png" width="600" />
