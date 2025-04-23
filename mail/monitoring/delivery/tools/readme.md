## Использование resource_manager:
### Просмотр версий ресурса:
```
$ resource_manager.py view -n yamail-mx-monitor
1057171780	2019-08-02 16:32:28	yamail-mx-monitor.1.2.0-5422152.tar.gz
1055557658	2019-08-01 14:57:03	yamail-mx-monitor.1.2.0-5387197.tar.gz
1053853256	2019-07-31 13:42:35	yamail-mx-monitor.1.2.0-5385892.tar.gz
1050770078	2019-07-29 14:32:07	yamail-mx-monitor.1.2.0-5371221.tar.gz
1050508713	2019-07-29 11:18:41	yamail-mx-monitor.1.2.0-5370479.tar.gz
1044873292	2019-07-24 18:49:07	yamail-mx-monitor.1.2.0-5350806.tar.gz
1036337075	2019-07-18 13:23:17	yamail-mx-monitor.1.2.0-5318652.tar.gz
1029182306	2019-07-12 20:24:30	yamail-mx-monitor.1.2.0-5296522.tar.gz
1029058597	2019-07-12 18:59:26	yamail-mx-monitor.1.2.0-5296264.tar.gz
1028676302	2019-07-12 14:48:10	yamail-mx-monitor.1.2.0-5295225.tar.gz
```
### Обновление ресурса в окружении Qloud:
Из-за особенностей API Qloud обновлять ресурс можно только на уровне окружения.
Скрпит ищет ресурс по имени среди ресурсов компонентов окружения и обновляет его для соотвествующих компонентов.

Для работы нужен Qloud oauth token. Его можно указать в окружении "QLOUD_TOKEN" или записать в файл ~/.config/qloud_token
Токен можно получить [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=072224ad7c864b158601e49b25497eac).

#### Деплой во все окружения Доставки:
```
$ resource_manager.py deploy -E <файл со списком окружений> -n <имя ресурса> -r <ревизия ресурса>
$ resource_manager.py deploy -E envs.prod -n <имя ресурса> -r <ревизия ресурса>
```

#### Деплой на конкретное окружение Доставки:
```
$ resource_manager.py deploy -e <имя окружения в Qloud> -n <имя ресурса> -r <ревизия ресурса>
$ resource_manager.py deploy -e mail.mdbsave-corp.production -n yamail-mx-monitor -r 1057171780
resource yamail-mx-monitor will be updated for save
root['components'][0]['sandboxResources'][0]['id']
{'new_value': 1057171780, 'old_value': 985253517}


{u'admin': True,
 u'applicationName': u'mdbsave-corp',
 u'author': u'pierre',
 u'comment': u'',
 u'creationDate': u'2019-08-02T20:30:27.234+0300',
 u'engine': u'platform',
 u'name': u'production',
 u'objectId': u'mail.mdbsave-corp.production',
 u'projectName': u'mail',
 u'status': u'NEW',
 u'statusMessage': u'',
 u'version': 1564767027234}
```
