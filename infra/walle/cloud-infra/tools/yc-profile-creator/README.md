# Create yc and ycp profiles tuned to service account.

This script creates:
* Wall-e service account's IAM key for current user
* `yc` profile with this key

ycp profile must be created manually.


## Prerequisites
* `yc` installed and set up with federative account
* `ycp` installed

## Usage

1. Check that federative profiles exist:
```
[ ~ ] $ yc config profile list
preprod-fed-user
prod-fed-user ACTIVE
[ ~ ] $
```

2. Run `./create-walle-main-sa-yc-profile -s prod`:
```
$ ./create-walle-main-sa-yc-profile -s prod
* Creating IAM key for service account "yc.wall-e.main-sa"...
...

* Done.
* Creating yc profile "prod-yc.wall-e.main-sa" for service account "yc.wall-e.main-sa"...
Profile 'prod-yc.wall-e.main-sa' created and activated
* Done.
* Configuring yc profile "prod-yc.wall-e.main-sa"...
* Done.

* Your key is in file '/home/squirrel/prod_yc.wall-e.main-sa_key.json'.    'cut' the key, copy it, and paste it in YCP config file ~/.config/ycp/config.yaml .    Example of YCP config file: ycp_config_example.yaml
$
```

3. `cat` the key file and copy everything into buffer.
4. Open ycp config file `~/.config/ycp/config.yaml`, and paste key contents from buffer into corresponding section. See example file [ycp_config_example.yaml](ycp_config_example.yaml).
5. Run `./create-walle-main-sa-yc-profile -s preprod` and repeat steps 3 and 4 for new key and ycp profile.
6. Run `./create-walle-main-sa-yc-profile -s testing` and repeat steps 3 and 4 for new key and ycp profile.
7. Check that everything is configured right:
```
$ yc dns zone list --profile prod-yc.wall-e.main-sa
$ ycp dns v1 dns-zone list --profile prod-yc.wall-e.main-sa
$ yc dns zone list --profile preprod-yc.wall-e.main-sa
$ ycp dns v1 dns-zone list --profile preprod-yc.wall-e.main-sa
$ yc dns zone list --profile preprod-yc.wall-e.main-sa-testing
$ ycp dns v1 dns-zone list --profile preprod-yc.wall-e.main-sa-testing
```
