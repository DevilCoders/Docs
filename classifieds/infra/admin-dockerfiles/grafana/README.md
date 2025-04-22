# Grafana docker build

Наша сборка докерфайла графаны

- авторизация через паспорт (auth-proxy)
- ручки ping/metrics для деплоя в shiva

## auth-proxy

Авторизационный сервис для envoy (ходит на каждый запрос в него и проверяет авторизацию):
- ищем "Authorization: OAuth <token>"
- ищем куки session_id/sessionid2
- авторизуем через ЧЯ или редиректим на паспорт
