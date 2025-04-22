# TrainNmt

Задача для запуска процесса обучения нейросетевого перевода в Нирване


Пример запуска для отладки:
```
./train_nmt run -o MT --type TRAIN_NMT '{"custom_fields": [{"name":"direction", "value":"lv-en"}, {"name":"build_vocs", "value": true}, {"name":"secret", "value": "sec-01dws6hkyab1sn1mx6b7e7m7pg"}]}'
```

Перед отладочным запуском стоит удалить наследование от LastBinaryTaskRelease, без этого изменения могут не подцепиться.
