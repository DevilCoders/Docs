## Решение проблем

## Templar / Kotik
### При запуске пишет, что порт занят
```bash
lsof -i :3333    # выплюнет процесс, см. у него PID
kill -9 <PID>    # гасим процесс
```

### JavaScript heap out of memory
Для сборки указываем дополнительный параметр:
```bash
NODE_OPTIONS="--max_old_space_size=4096"
```

### Не работает туннель
Можно попробовать изменить адрес через параметр:
```bash
TUNNELER_HOST=ws2-tunnelerapi.tunneler-si.yandex-team.ru
```
