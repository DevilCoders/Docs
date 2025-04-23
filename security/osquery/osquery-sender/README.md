# osquery-sender

This is an endpoint, which converts json sent by osquery to json accectable by splunk hatch.

### Environment variables:

`SPLUNK_TOKEN` - token to pass in Authorization header

`SPLUNK_URL` - URL to forward messages

`PORT` - port to bind. Default value is 443

### Update config

config currently exists as qloud secret. it can not be viewed from outside the container by design,
but it can be read from the instance itself just ssh inside and `cat /config/config.yaml`.

secret is located [here](https://qloud-ext.yandex-team.ru/secrets/secret.osquery-sender-config-yaml)

secret example [can be found here](https://a.yandex-team.ru/arc/trunk/arcadia/junk/e-sidorov/osquery-local-cfg/config-local.yaml)

current secret looks like [that](https://wiki.yandex-team.ru/users/shashial/osquery/osquery-sender/#config)


### How to update container and push to registry:

[docker registry instruction](https://wiki.yandex-team.ru/qloud/docker-registry/)

- token can be obatained [here](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
- get tag list:
    ```<space_> export OATH='<token>'```

    ```curl -H "Authorization: OAuth $OATH" -v https://registry.yandex.net/v2/security/osquery-sender/tags/list```

- build and push container to registry:
    ```go build
    docker login -u shashial -p <token> registry.yandex.net
    docker build . --force-rm
    docker images
    docker tag <tag> registry.yandex.net/security/osquery-sender:2019-06-24T16.16
    docker push registry.yandex.net/security/osquery-sender```

### Syslog parsing

See [syslogparsing/README.md](syslogparsing/README.md).
