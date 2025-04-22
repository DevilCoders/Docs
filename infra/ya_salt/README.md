# HOSTMAN aka ya-salt

[ABC](https://abc.yandex-team.ru/services/hostmanager)
[Wiki](https://wiki.yandex-team.ru/runtime-cloud/salt/)
[Startrek](https://st.yandex-team.ru/HOSTMAN)

## In case of emergency

Try to reach [duty engineer](https://abc.yandex-team.ru/services/hostmanager/duty/)  
See disaster recovery plans [docs/EMERGENCY.md](docs/EMERGENCY.md)

## Directory tree
 * `bin` - directory with ya-salt executables
 * `docs` - documentation
 * `hostmanager` - hostmanager source files
 * `lib` - utility source files
 * `motd` - message of the day binary project
 * `panels` - YASM panels definitions
 * `pkg` - .deb packages definitions and files
 * `postinst` - postinst executable project for host agent
 * `proto` - protobuf definitions
 * `vendor` - cut and mangled original salt
 * `README.md` - docs

### `postinst`
Contains postinst executable run by dpkg to install package and utilities for manual testing salt (very early and ugly).
As of today:
```
# Run this from infra/ya_salt
sudo docker run -t -v $(pwd):/salt -v ${HOME}/.ya:${HOME}/.ya ubuntu:16.04 /salt/postinst/tests/test-postinst-systemd-fresh.sh
sudo docker run -t -v $(pwd):/salt -v ${HOME}/.ya:${HOME}/.ya ubuntu:16.04 /salt/postinst/tests/test-postinst-systemd-update.sh
```
This will run docker container bind-mounting salt directory and 
`.ya` directory (with build artifacts) and check if postinst executed normally.

## Initial setup
After host has been fully set up, we need to reboot it to apply all settings, namely interrupts spread. To perform this
we have initial setup machinery implemented in hostmanager. It works as follows.

When host is being redeployed `yandex-search-salt` package is installed during host setup procedure.
In postinst scriptlet during fresh install we put special flag file (`__need_initial_setup__`) on filesystem which
makes `ya-salt` execution to check if:
  * we have switched from `base` salt environment
  * kernel is ready
  * salt executed and we have no failed states

If all prerequisites are in place, initial setup routine sets `need_reboot` flag in it's status.

Reboot manager (runs after every execution) performs check via orly rule `hostman-initial-{production,prestable}` and 
if orly allows operation - initiates node reboot.

## Feedback

Feel free to [create issue](https://st.yandex-team.ru/createTicket?type=1&priority=2&queue=HOSTMAN)
if you spotted a bug or have a feature request.
