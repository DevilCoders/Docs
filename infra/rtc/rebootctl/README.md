## About
`rebootctl` is a tool for controlled and reproducible but still **manual** host reboots as apposed to manual reboots done with
BASH foo, sky lists, yr and other undocumented facilities.

## Usage
Proposed user workflow looks like this:
  * Write script for planned reboots and show it to "host owners".
  It can be done via Arcanum PR.
  * Commit it in `./scripts`.
  * Run `./bin/rebootctl script -f scripts/{your-script}.yaml`.
  Don't forget to export `WALLE_TOKEN=` beforehand.
  To obtain this token, please visit [OAuth](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9e9702c0b7f54152ac339989d9039ccd)
  * Follow instructions and watch status, rendered on screen.
