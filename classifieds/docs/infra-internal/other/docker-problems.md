# Траблшутинг docker

## Docker не стартует на железе

Если докер на железных хостах не стартует, проверяем лог docker (`journalctl -u docker`). При возникновения такой ошибки:
```
Error starting daemon: Error initializing network controller: Error creating default "bridge" network: failed to allocate secondary ip address (DefaultGatewayIPv6:<ipv6addr>): Address already in use
```

выполняем следующие действия:
```
mv /etc/docker/daemon.json /var/tmp/daemon.json
service docker restart
mv /var/tmp/daemon.json /etc/docker/daemon.json
service docker restart
```
