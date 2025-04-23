# mesh-control
service mesh control plane

## Disclaimer

Работает поверх [envoyproxy/go-control-plane](https://github.com/envoyproxy/go-control-plane).
### Принцип работы
- собирает карту и список запущенных сервисов из шивы раз в N сек
- следит за сервисами в консуле
- следит за сертификатами
