# strm-auto-ticket
Creates ticket in STREAMSUP queue.

## Usage
```
strmticket -h

```

Settings are loaded from 'strmticket.conf' file.
Token is loaded from 'strmticket.oauth' file.
YT-Token is loaded from 'strmticket.yttoken' file.
Telegram Token (optional) is loaded from 'strmticket.tgtoken' file.

Config and tokens locations: current dir, 
/etc/[strmticket], /usr/local/etc/[strmticket].

## Command line options 

### -c --cron
For tests or running via cron|systemd-timer.
Parses channel-tumbler for channels that are broken > N hours and creates tickets.

### -d --daemon
Runs web-server and scheduled tasks


## Development and contributing

Provide token and config (cp and edit samples).
Oauth token must have access to ST, Juggler, Staff, Calendar, ABC.
YT Token must have access in YT to hahn [strmduty](https://yt.yandex-team.ru/hahn/navigation?path=//home/strmduty) namespace (locks and db) and [radiodata table](https://yt.yandex-team.ru/hahn/navigation?path=//home/muzsearch/fm_radio/radio_data&offsetMode=row)


```bash
# Calendar API dirty hack
ssh -f -N -L 1080:calendar-api.tools.yandex.net:80 guardian.search.yandex.net

# Build and run strmticket in project root

ya make . && mv strmticket/strmticket strmticket_exe && strmticket_exe -d