# Hostman server
Server component which syncs salt repo from VCS and serves via HTTP to cloud hosts.

## Branches
Each server must serve particular branch. E.g. stout24 serves SAS branch.

We use systemd as supervisor and systemd drop-ins to keep .deb package constant and allow customization.

Thus to start hm-server and point it to `master_sas` branch we configure `/etc/systemd/system/yandex-hm-server.service.d/30-settings.conf`
with following contents:
```
[Service]
Environment=HM_REMOTES=saltstack,sysdev,core
Environment=HM_ROLE=(sas|vla|man|msk|prestable)
```
and call `systemctl daemon-reload` to re-read configuration. After that we (re)start hm-server: `systemctl start yandex-hm-server`.

## Logs
For simplicity hm-server logs to stdout and it's unit file directs systemd to forward it to journal. Thus to see logs
one must use `journalctl -u yandex-hm-server`.

# Bootstrap host
In order to manually //bootstrap// hm-server on host we need:
  * Execute `apt-get install yandex-hm-server`
  * Get OAuth token from [YAV secret](https://yav.yandex-team.ru/secret/sec-01dh47m6axbcbgk1jmr286rvj4)
  * Log into physical/virtual node as root and invoke `echo 'BB_OAUTH_TOKEN={TOKEN}' > /etc/hm-server-env.conf`
  * Configure role (via drop-in `/etc/systemd/system/yandex-hm-server.service.d/30-settings.conf`):
```
[Service]
Environment=HM_REMOTES=saltstack,sysdev
Environment=HM_ROLE=(sas|vla|man|msk|prestable)
```
  * Invoke `systemctl daemon-reload`
  * Start service `systemctl restart yandex-hm-server`



To provision all servers: `sky run "echo 'BB_OAUTH_TOKEN=<TOKEN-VALUE>' > /etc/hm-server-env.conf" G@ALL_STOUT`.

### Acquire OAuth token
If token has expired or revoked:
  * Copy [robot-infrasearch](https://staff.yandex-team.ru/robot-infrasearch) [password](https://yav.yandex-team.ru/secret/sec-01dgz5pcfve6572hrfc04kyjt1) to clipboard.
  * Acquire token by visiting [this url](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5476ddc0b4294eadbb2c19036ce89159) in incognito mode.
  * Save it into this [YAV secret](https://yav.yandex-team.ru/secret/sec-01dh47m6axbcbgk1jmr286rvj4)
