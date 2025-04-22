# Appmetrika API

{{TOC}}

## About
Позволяет загружать, удалять и читать тестовые устройства трекера AppMetrika.
[https://st.yandex-team.ru/MOPER-135](https://st.yandex-team.ru/MOPER-135)
[WIKI](https://wiki.yandex-team.ru/users/graev/Zagruzka-testovyx-ustrojjstv/)

## Token
AQAAAAAME5e9AAQtFSHcw5TMCUTxkWqc_UeNwgQ

## Usage
### Get test devices list with cURL:
```bash
curl "https://api.appmetrica.yandex.ru/management/v1/application/10321/testdevices?oauth_token=AQAAAAAME5e9AAQtFSHcw5TMCUTxkWqc_UeNwgQ" | python -m json.tool
```

### With [python-tool](https://a.yandex-team.ru/arc/trunk/arcadia/analytics/atom/trackers/metrica_api.py)

#### Examples
Example 1. *List test-devices*:
```python
from metrica_api import Metrika
metrica = Metrika()
metrica.list_devices(app_id=19531)
```
___
Example 2. *Add new devices*
```python
from metrica_api import Metrika
metrica = Metrika()

for xi, gaid in enumerate(gaids):
    if gaid not in ppandroid_10321_device_ids:
        metrica.add_device(
	          app_id=10321,
	          device_id=gaid,
	          name='t{}'.format(str(xi+80)),
	          type='google_aid',
	          purpose='reattribution'
				)
```
[https://paste.yandex-team.ru/225072](https://paste.yandex-team.ru/225072)
___
Example 3. *Register new devices as toloka skill*
```python
from tolokahelper import TolokaHelper
th = TolokaHelper(date='2017-04-07')

with open('gaid_imei_aid_workerid_filtered.tsv') as fp:
    worker_ids = [line.split('\t')[-1].strip() for line in fp.readlines() if line != '\n']

for worker_id in worker_ids:
    th.tlk.set_worker_skill(
		    skill_id=3871,
		    user_id=worker_id,
		    value=1
		)
```
[https://paste.yandex-team.ru/225953](https://paste.yandex-team.ru/225953)
___
Example 4. *Change possible gaids in toloka project options*
```python
from tolokahelper import TolokaHelper
th = TolokaHelper('lol')
project_4899 = th.tlk.project(4899)

with open('gaid_imei_aid_workerid_filtered.tsv') as fp:
    gaids = []
    for line in fp:
        gaids.append(line.split('\t')[0])

project_4899['task_spec']['output_spec']['gaid']['allowed_values'] = list(set(gaids))
th.tlk.api.put('/projects/4899', data=project_4899)
```
[https://paste.yandex-team.ru/226988](https://paste.yandex-team.ru/226988)