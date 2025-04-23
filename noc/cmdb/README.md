# CMDB

Network configuration storage and management system

## Configuration

### <a name="testing"></a> Testing
https://a.yandex-team.ru/arcadia/admins/salt-media/noc/pillar/nocdev-test-cmdb.sls
```bash
$ executer
> p_exec %nocdev-test-cmdb sudo salt-call --state-output=changes --state-verbose=False -l critical state.highstate
> p_exec %nocdev-test-cmdb sudo service cmdb restart
```

### Production
https://a.yandex-team.ru/arcadia/admins/salt-media/noc/pillar/nocdev-cmdb.sls
```bash
$ executer
> p_exec %nocdev-cmdb sudo salt-call --state-output=changes --state-verbose=False -l critical state.highstate
> p_exec %nocdev-cmdb sudo service cmdb restart
```

## Database

[Testing cluster](https://yc.yandex-team.ru/folders/foosk13mu0ib9qrjkh8a/managed-postgresql/cluster/mdbqiedl2sfb1v628r9u?section=overview)

[Production cluster](https://yc.yandex-team.ru/folders/foosk13mu0ib9qrjkh8a/managed-postgresql/cluster/mdbqiedl2sfb1v628r9u?section=overview)


## IDM system

Testing: https://idm.yandex-team.ru/system/cmdb-testing/

Production: https://idm.yandex-team.ru/system/cmdb/

## Swagger
### Swagger UI

Testing: https://cmdb-test.yandex.net/docs

Production: https://cmdb.yandex.net/docs

### Generate swagger spec

```bash
ya make -t pkg/swaggermur  # test updates swagger.json
```

### Documentation for swagger markdown in docstrings

https://goswagger.io/use/spec.html

## CLI

```bash
cmd/cmdb/cmdb link-details post -c 'http://cmdb-test.yandex.net' -p 'https://racktables.yandex-team.ru/export/peers-report.php?format=json'
```

### Generate tickets for CLI


```bash
ya tool tvmknife get_user_ticket sshkey --tvm_id 2030827 > ~/.cmdb/user_ticket; ya tool tvmknife get_service_ticket sshkey --src 2030827 --dst 2030827 > ~/.cmdb/service_ticket 
```

## Create racktables testing

```bash
git clone git@noc-gitlab.yandex-team.ru:nocdev/rt-docker.git
cd rt-docker/noc/rttestctl/cmd/rttctl/
make build
./cmd/rttctl/rttctl.linux spawn --ttl 2190h --branch master --rw --update
./cmd/rttctl/rttctl.linux ps
```

Then update sandbox task: https://sandbox.yandex-team.ru/scheduler/697961/view

Then update [testing config](#testing)

IMPORTANT: For mutations to work on testing, you need to set permissions, talk to @moonug or @mocksoul  
TODO: make them fix this
