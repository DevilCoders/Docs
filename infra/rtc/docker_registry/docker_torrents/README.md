# Docker Registry Torrents

This daemon bakes rbtorrents from docker/distribution layers

## CMD

### Build

```bash
ya make
```

### Usage

```
usage: docker_torrents [-h] [-c CONFIG] [-d [DEBUG]]

Process some integers.

optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG, --config CONFIG
                        Config file (default /etc/docker-registry-
                        torrents/config.yaml)
  -d [DEBUG], --debug [DEBUG]
                        Enable debug mode in Flask
```

### Config example

```yaml
application:
    port: 10050
    host: '::'
    event_authorization: 'secretkey'
docker_registry:
    host: 'registry-int.yandex.net'
    proto: 'https'
    image_resolve_template: '{proto}://{host}/v2/{scope}/manifests/{tag}'
    hash_resolve_template: '{proto}://{host}/v2/{scope}/blobs/{blob_sum}'
    tags_resolve_template: '{proto}://{host}/v2/{scope}/tags/list'
    blob_sum_prefix: 'sha256:'
    compatibility_header: 'application/vnd.docker.distribution.manifest.v2+json'
    connect_timeout: 0.2
    read_timeout: 2
blackbox:
    url_template: 'https://blackbox.yandex-team.ru/blackbox?{payload}'
    scopes: 'registry:use'
    connect_timeout: 0.2
    read_timeout: 0.5
mds:
    url_template: 'http://storage-int.mds.yandex.net:80/{payload}/'
    namespace: 'docker-registry'
    torrent_url: 'http://rbtorrent.front.intape.yandex.net/announce'
    connect_timeout: 0.5
    read_timeout: 600
brewer:
    brew_discard_timeout: 300
    sleep_time: 10
    layers_per_chunk: 10
    brew_user: 'robot-qloud-client'
db:
    database: 'database_name'
    username: 'database_login'
    password: 'P@ssw0rd'
    host: 'host1,host2,host3'
    port: 6432
    table_name: 'rbtorrent_mapping'
    old_table_name: 'mds_keys_to_rbtorrents_mapping'
    blob_path_template: '/docker/registry/v2/blobs/sha256/{short_digest}/{full_digest}/data'
    blob_path_digest_index: 7
    mfs_table: 'mfs'
    mds_table: 'mds'
    max_pool_size: 100
    connect_timeout: 0.1
```

## API

### Get manifest

```GET /v2/<scope>/manifests/<tag>```

Mandatory headers:
```
X-Real-IP: <user_ip>
Authorization: <User oauth token with registry:use scope>
```

#### Description

Service produces exact request to docker/distribution with header```Accept: application/vnd.docker.distribution.manifest.v2+json```
but appends ```rbtorrent_id``` for each layer if it exists in database or puts layer to brew queue if it's not.

#### Example

Request:
```http request
 GET /v2/ubuntu/manifests/precise
```
Response:

```json
{
  "schemaVersion": 2,
  "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
  "config": {
    "mediaType": "application/vnd.docker.container.image.v1+json",
    "size": 5013,
    "digest": "sha256:50e7fb0ef7a7859ff5c021ef83943bf1c20672bd39cb0566ae14212ed15d4676"
  },
  "layers": [
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 40000566,
      "digest": "sha256:8af661395bb22734e6f7a4f2b71a3847e458e0e32c66cf24e4aba86a60bfbf1c",
      "rbtorrent_id": "rbtorrent:ad6ace9412876f9c2928bb5ba770b36019294536"
    },
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 58971,
      "digest": "sha256:a9eddfc29172122f3d693c910f3a2099d559cecc707a6eece94ba2fec6b1c0b2",
      "rbtorrent_id": "rbtorrent:c0e2ada473bd8a152f440cf16e745e532d7ed57d"
    },
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 416,
      "digest": "sha256:c02b8a6855f30647b4a17b7cd1124abf49017f7764fa54655fcc429a52597c16",
      "rbtorrent_id": "rbtorrent:3eb49dea7a12cccd4e5325efc4ee0c057b6b0f4e"
    },
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 674,
      "digest": "sha256:74f129d191bdc061821e5db6eb0a14fe940a88812d711a1f1ccb486129498a76",
      "rbtorrent_id": "rbtorrent:7a261daac4a4ff27f6729db62794a3dadaab570d"
    },
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 163,
      "digest": "sha256:119bcef3e410483965feb31552398346ce7c7b6d6f0e88a86bd891034d052268",
      "rbtorrent_id": "rbtorrent:66caa7c1965c06528325d0a25d955e7d5e17cde8"
    },
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 405,
      "digest": "sha256:431e19a6c84650ab3f88519857b1df75a54906dac19419b4ce3dfb30599a9c21",
      "rbtorrent_id": "rbtorrent:e0e47e9df8edb0ad5a50e2d968990c6ea1ee4e44"
    },
    {
      "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
      "size": 87394128,
      "digest": "sha256:299c3ccb439d1ec1b9d8d561f9864cb9ccaaefabb117a4dd03faef49ca7edce5",
      "rbtorrent_id": "rbtorrent:702a52634dd7c57e0c6730755f3e5d3d535ba1a3"
    }
  ]
}
```

### Event

```POST /v0/event```

#### Description

[Event](https://docs.docker.com/registry/notifications/) listener from docker/distribution

Puts new layers to brew queue if repository has rbtorrent role

#### Example

Request:
```http request
 POST /v0/event
```

Data:
```json
{
   "events": [
      {
         "id": "asdf-asdf-asdf-asdf-0",
         "timestamp": "2006-01-02T15:04:05Z",
         "action": "push",
         "target": {
            "mediaType": "application/vnd.docker.distribution.manifest.v1+json",
            "length": 1,
            "digest": "sha256:fea8895f450959fa676bcc1df0611ea93823a735a01205fd8622846041d0c7cf",
            "repository": "library/test",
            "url": "http://example.com/v2/library/test/manifests/sha256:c3b3692957d439ac1928219a83fac91e7bf96c153725526874673ae1f2023f8d5"
         },
         "request": {
            "id": "asdfasdf",
            "addr": "client.local",
            "host": "registrycluster.local",
            "method": "PUT",
            "useragent": "test/0.1"
         },
         "actor": {
            "name": "test-actor"
         },
         "source": {
            "addr": "hostname.local:port"
         }
      },
      {
         "id": "asdf-asdf-asdf-asdf-1",
         "timestamp": "2006-01-02T15:04:05Z",
         "action": "push",
         "target": {
            "mediaType": "application/vnd.docker.container.image.rootfs.diff+x-gtar",
            "length": 2,
            "digest": "sha256:c3b3692957d439ac1928219a83fac91e7bf96c153725526874673ae1f2023f8d5",
            "repository": "library/test",
            "url": "http://example.com/v2/library/test/blobs/sha256:c3b3692957d439ac1928219a83fac91e7bf96c153725526874673ae1f2023f8d5"
         },
         "request": {
            "id": "asdfasdf",
            "addr": "client.local",
            "host": "registrycluster.local",
            "method": "PUT",
            "useragent": "test/0.1"
         },
         "actor": {
            "name": "test-actor"
         },
         "source": {
            "addr": "hostname.local:port"
         }
      },
      {
         "id": "asdf-asdf-asdf-asdf-2",
         "timestamp": "2006-01-02T15:04:05Z",
         "action": "push",
         "target": {
            "mediaType": "application/vnd.docker.container.image.rootfs.diff+x-gtar",
            "length": 3,
            "digest": "sha256:c3b3692957d439ac1928219a83fac91e7bf96c153725526874673ae1f2023f8d5",
            "repository": "library/test",
            "url": "http://example.com/v2/library/test/blobs/sha256:c3b3692957d439ac1928219a83fac91e7bf96c153725526874673ae1f2023f8d5"
         },
         "request": {
            "id": "asdfasdf",
            "addr": "client.local",
            "host": "registrycluster.local",
            "method": "PUT",
            "useragent": "test/0.1"
         },
         "actor": {
            "name": "test-actor"
         },
         "source": {
            "addr": "hostname.local:port"
         }
      }
   ]
 }
```

Response:

```OK```

## Database scheme

```postgresql
CREATE TABLE IF NOT EXISTS rbtorrent_mapping (
    digest varchar(128) PRIMARY KEY,  --layer digest
    rbtorrent_id varchar(64),          --layer rbtorrent, main point of service
    added BIGINT,                     --timestamp when record was added
    brew_lock BIGINT,                 --timestamp to lock layer for brewing
    brewed BIGINT);                   --timestamp when layer brewed
CREATE UNIQUE INDEX IF NOT EXISTS rbtorrent_mapping_rbtorrent_idx ON rbtorrent_mapping USING btree (rbtorrent_id);
CREATE INDEX IF NOT EXISTS rbtorrent_mapping_added_sort ON rbtorrent_mapping USING btree (added);
CREATE INDEX IF NOT EXISTS rbtorrent_mapping_brew_lock_compare ON rbtorrent_mapping USING btree (brew_lock);
CREATE INDEX IF NOT EXISTS rbtorrent_mapping_brew_lock_null ON rbtorrent_mapping(brew_lock) WHERE brew_lock IS NOT NULL;
CREATE INDEX IF NOT EXISTS rbtorrent_mapping_brewed_null ON rbtorrent_mapping(brewed) WHERE brewed IS NOT NULL;
```

## Links

* [ABC](https://abc.yandex-team.ru/services/dockerregistry/)
* [Monitoring](https://yasm.yandex-team.ru/panel/docker_registry)