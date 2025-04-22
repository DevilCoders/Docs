# Утилиты

Утилиты для упрощения разработки и поддержки Маркета для бизнеса

## Как подключить

В домашней директории пользователя в ```.profile``` добавьте следующую строку (после добавление потребуется
перезапустить терминал или перезалогиниться)

```bash
PATH="$PATH:$HOME/arcadia/market/b2b/bin"
```
(Если у вас Аркадия монитируется по другому пути, то укажите правильный путь)

## Доступные утилиты

tvm_curl - позволяет выполнять запросы с использованием service tvm ticket. Важно: вам потребуется иметь роль "TVM ssh пользователь" для
  сервиса от имени которого делается запрос. Пример использования:
  ```bash
  SRC=2031863 DST=2031865 tvm_curl https://service/path
  ```

b2bc_curl - позволяет выполнять запросы к проду бабуси
  ```bash
  b2bc_curl http://marketb2bclients.vs.market.yandex.net/users/4002117333/customers
  ```

b2bc_users_check - дергает продовую ручку users/${uid}/check
  ```bash
  b2bc_users_check 1234 # 1234 - uid пользователя
  b2bc_users_check vasya.pupkin # vasya.pupkin - логин пользователя
  ```

b2bc_users_check - дергает продовую ручку users/${uid}/customers
  ```bash
  b2bc_users_customers 1234 # 1234 - uid пользователя
  b2bc_users_customers vasya.pupkin # vasya.pupkin - логин пользователя
  ```

uid_by_login - возвращает uid пользователя по его логину
  ```bash
  uid_by_login vasya.pupkin # vasya.pupkin - логин пользователя
  ```
