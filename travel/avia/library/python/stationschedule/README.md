stationschedule
===============

Библиотека получения расписания по станции

Переводы
--------

Переводы лежат в stationschedule/xgettext/keyset.json, кейсет в танкере xgettext:stationschedule.

Для подключения переводов в вашем проекте в settings.py нужно прописать:

```python
XGETTEXT_KEYSETS.update({
    'stationschedule': {
        'filename': 'stationschedule/xgettext/keyset.json',
        'dirs': [
            'stationschedule',
        ]
    }
})
```
