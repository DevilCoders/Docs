bugbounty
=========

Deploy external:
```
RELEASER_PROJECT_CONFIG=".release.external.hjson" releaser release
```

Deploy internal:
```
RELEASER_PROJECT_CONFIG=".release.internal.hjson" releaser release
```

Translations:
```
docker-compose run extback extback compilemessages
docker-compose run intback intback compilemessages
```
