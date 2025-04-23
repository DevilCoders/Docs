## 0.3.5

* Add `tvmtool` APIv2 endpoint `/v2/roles` support - `client.getRoles()`

## 0.3.3

* Don't log response bodies from TVM daemon ([75ba847b72a2332edcf248e54d64e2ad5cbecc37](https://github.yandex-team.ru/maps/tvm/commit/75ba847b72a2332edcf248e54d64e2ad5cbecc37)).

## 0.3.2

* Include `src/lib` to npm package for source maps.

## 0.3.1

* Use inline source maps.

## 0.3.0

### Breaking changes

* Rename interfaces ([#7](https://github.yandex-team.ru/maps/tvm/issues/7)):
  * `ServiceInfo -> ServiceTicketInfo`
  * `UserInfo -> UserTicketInfo`

### New features

* Add user ticket support ([#3](https://github.yandex-team.ru/maps/tvm/issues/3)).
