# kadavr-test-scripts

Наборы скриптов для устновки стейта кадавра для страниц и просто функционала

## Зачем?

Чтобы проверять стейт кадавра прямо в браузере перед автотестами.
Это быстрее чем запускать автотесты.

## Usage

Нужно задавать `kadavr_host`, `kadavr_port` именно lowercase

```
kadavr_host=logrus01hd.market.yandex.net \
kadavr_port=10090 \
node src/spec/hermione/kadavr-test-scripts/yandexGo/setupYandexGoProductPage.js
```
