# What is it?
Balance FOP web server

# Qloud
## Logs
### Testing
* https://solomon.yandex-team.ru/?project=logbroker&cluster=logbroker&service=logbroker&l.ident=paysys-balance-fop-test&l.host=cluster&l.topic=*&l.sensor=BytesReceived&graph=auto&b=1h&e=
* https://yt.yandex-team.ru/hahn/?page=navigation&path=//home/logfeller/logs&filter=fop
## Deploy
Based on [releaser](https://github.yandex-team.ru/tools/releaser).
DON'T FORGET TO SETUP OAUTH TOKEN IN `~/.release.hjson`!

```bash
$ Status
releaser status

# Testing
releaser deploy \
    -e testing \
    -v 1.0.30-1.0.295 \
    -dcf "StarTrek issue key"

# Production
releaser deploy \
    -e production \
    -v 1.0.30-1.0.295 \
    -dcf "StarTrek issue key"
```

# How to run
```./gradlew run```

# Similar:
https://github.com/zilverline/apache-fop-server

# How to test:
```curl -X POST --data '<invoices><invoice><offer-type>17</offer-type><agreement-only>1</agreement-only></invoice></invoices>' 'http://localhost:30101/render?entrypoint=default&outputformat=fo_out'```

# Performance hints
https://xmlgraphics.apache.org/fop/2.1/embedding.html#performance
