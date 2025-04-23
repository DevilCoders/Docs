# How-to: Yubikey

Если говорить кратко, то [Yubikey](https://www.yubico.com/) это хардварный токен, который умеет работать как смарт-карта и предоставлять MFA/беспарольную аутентификацию (FIDO U2F, FIDO2). Нас в первую очередь интересует использование оного в качестве смарт-карты.

## Получить Yubikey {#new-yubikey}
Если у вас еще нет yubikey, то его можно получить или в [Хелпоматах](https://help.yandex-team.ru/?form=463&search=) в офисе (если токенов в нём не окажется, обратитесь к дежурному в welcome-зоне вашего офиса) или заказать на [портале Service Desk](https://help.yandex-team.ru/?form=498&search=&skip_service_card=true).

В данный момент выдаётся два типа YubiKey:
  - [YubiKey 5 Nano Type A](https://www.yubico.com/us/product/yubikey-5-nano/)
  - [YubiKey 5 Nano Type C](https://www.yubico.com/us/product/yubikey-5c-nano/)

Вы можете взять тот тип YubiKey, который вам больше подходит и нравится. Пожалуйста, если берете "YubiKey 5 Nano Type A", вставляйте его правильной стороной :) Легко не заметить.

## Если вы заказали доставку Yubikey, но он еще не приехал {#softkeyring}
Skotty умеет работать с софтварным хранилищем, для этого достаточно использовать аргумент `--any-keyring` при первичной настройке и он предложит альтернативы Yubikey в зависимости от вашей OS.
Например:
```
% skotty setup --any-keyring
[i] initialize keyring
? Select Keyring:  [Use arrows to move, type to filter]
> Keychain
  Files
```

Учтите, что это временная мера и после приезда Yubikey нужно будет перенастроить skotty на его использование (`skotty setup --keyring`).

## Перенастройка
Если вы желаете перенастроить Yubikey (будь то новый или б/у) необходимо выполнить `skotty setup --keyring` и пройти мастер.
В ходе настройки будут:
  - сгенерированы все нужные приватные ключи: `renew` + `secure` + `insecure` + `legacy` + `sudo`
  - получены соответствующие сертификаты
  - получен токен для дальнейшего обновления сертификатов
  - все это сохранится в конфиг и на диск

{% note warning %}
  
Генерация новых ключей означает, что предыдущий `legacy` ключ перестанет работать и его нужно будет обновить на стафф + дождаться выкатки.

{% endnote %}

{% note warning %}
  
Skotty сбрасывает (очищаются все PIV слоты, генерится новый PIN/PUK/Management key) все ранее неиспользованные Yubikey, показывая вам сгенерированный `PIN`/`PUK`. Сохраните `PUK` в надежном месте, он может понадобиться для разблокировки Yubikey в случае каких-либо проблем.

{% endnote %}

Пока процесс миграции не окончен, нужно самостоятельно добавить публичные ключи на страфф.

{% note info %}

Актуальный список ключей для добавления на стафф всегда можно получить с помощью: `skotty ssh keys`.

{% endnote %}

Пример прохождения мастера:
[![пример настройки](_assets/skotty_setup.png)](https://jing.yandex-team.ru/files/buglloc/skotty_setup.png?1)

## Посмотреть список токенов
Иногда бывает полезно посмотреть краткую информацию о всех Yubikey в системе (особенно, если их несколько), это можно сделать с помощью `skotty yubikey list`:
![yubikey list](_assets/skotty_yubikey_list.png)

## Разблокировать Yubikey
В случае, если вы забыли PIN, но у вас остался на руках PUK - Yubikey можно разблокировать (на это дается три попытки) c помощью `skotty yubikey unblock`.

## Сбросить Yubikey
Для сброса (очищаются все PIV слоты, генерится новый PIN/PUK/Management key) можно воспользоваться `skotty yubikey reset`:
![yubikey reset](_assets/skotty_yubikey_reset.png)

## Отключить/включить приложение Yubikey
Т.к. Yubikey это не просто смарт-карта, а еще ворох различных приложений (OTP, FIDO, etc), в skotty существует возможность включать или выключать оные.
Для примера, выключим OTP (это он печатает `ccccccuvrnvbjuhkebereerhltfeenejubclklnuetrn` при касании):
![yubikey disable OTP](_assets/skotty_yubikey_disable_otp.png)

## Сменить PIN
Если по каким-либо причинам вам не подходит автосгенерированный PIN, его можно сменить с помощью `skotty yubikey change-pin`. Который спросит текущий PIN (если сохраненный не подошел), спросит новый и все обновит:
![yubikey change-pin](_assets/skotty_yubikey_change_pin.png)

Требования к PIN: alphanumeric от 6 до 8 символов (ограничение Yubikey).
