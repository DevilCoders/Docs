Статика
-------
RASP_VAULT_STUB_SECRETS=1 common/virtualenv/bin/python manage.py collectstatic --noinput


Переводы.
---------
Для того, чтобы подключить переводы нужно:

1. Завести в танкере кейсет xgettext:morda_backend
2. Прописать common.xgettext в INSTALLED_APPS
3. Прописать в настройках:
```python
XGETTEXT_KEYSETS.update({
    'morda_backend': {
        'filename': 'morda_backend/xgettext/keyset.json',
        'dirs': [
            'morda_backend',
        ]
    }
})
```

Собрать переводы и загрузить их в танкер:
```bash
manage.py tankerupload xgettext:morda_backend
```

Выгрузить переводы из танкера:
```bash
manage.py tankerdownload xgettext:morda_backend
```


## Статика для django debug toolbar / restframework
```
./common/virtualenv/bin/python manage.py collectstatic
```

Теперь для всех ручек api, которые powered by djangorestframework доступна django-debug-toolbar.
