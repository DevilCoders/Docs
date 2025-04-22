Это мок утки на случай, если часть функционала утки ещё не реализована

Запускаем так:
python3 -m venv venv
source venv/bin/activate
python3 -m pip install -r ~/arc/arcadia/billing/yandex_pay/http_requests/mock/requirements.txt
mitmproxy -k -s ~/arc/arcadia/billing/yandex_pay/http_requests/mock/duckgo.mitmproxy.py

Проверяем:
curl -XGET http://duckgo.test/v1/sign_mastercard --data '{"body": "", "url": "", "method": "get"}'
Подпись настоящая
Только нужен доступ к секрету в yav
