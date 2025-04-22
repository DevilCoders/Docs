Фейковое API АРМ для разработки фронтенда. Умеет запускаться или как Аркадийное приложение:

```
ya make
./fake_sprav --port 44333
```

или как обычное Flask-приложение, чтобы можно было править без пересборки:

```
ya make -t --add-result=.py --add-result=.pyi --keep-going -xx -d --replace-result
FLASK_ENV=development PYTHONPATH=$ARCADIA_ROOT:$ARCADIA_ROOT/maps/doc/proto flask run --host :: --no-reload
```
