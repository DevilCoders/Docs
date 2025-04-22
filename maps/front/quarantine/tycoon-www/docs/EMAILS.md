# Вёрстка писем

Письма хранятся в сервисе [Рассылятор](https://sender.yandex-team.ru/yandex.spravochnik/)

Для работы нужно запросить права в [IDM](https://idm.yandex-team.ru/user/platosha/roles#rf=1,rf-role=0auvyVw7#sender/yandex.spravochnik/user(fields:()),rf-expanded=0auvyVw7,f-status=all,sort-by=-updated)

Под капотом рассылятор использует шаблонизатор [Jinja](https://jinja.palletsprojects.com/en/2.11.x/)
- https://wiki.yandex-team.ru/sender/anatomy/

### Как верстать
- Нужно клонировать [шаблон письма](https://sender.yandex-team.ru/yandex.spravochnik/campaign/325687/overview). (кнопка внизу)
- Далее "Сохранить и перейти к загрузке содержания"
- Далее "Править html" (если при правках будет ошибка, то сохранить шаблон не получится - бэк кинет ошибку и вы об этом узнаете)
- Чтобы прислать себе письмо нужно нажать кнопку "Опубликовать" и перейти на вкладку "Тест". Там будет пример `curl`, который надо выполнить, чтобы письмо пришло на почту.

Для верстки можно использовать VSCode Plugin [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)

### Для проверки писем
- [Can I Email](https://caniemail.com)
- Полезно жать кнопку "Переслать" в почте, так как после этого верстка часто ломается
- Послать письмо можно через Sender (смотри выше)
- Для отправки письма с переменными другому человеку, на вкладке "Тест", в поле "Адреса электронной почты" вносим данные в формате `{"email": "aleksbelov@yandex-team.ru", "var1": "value1", "var2": "value2"}`

### Тонкости
- обязательна табличная вёрстка
- не работают svg

### Чеклист
- проверить пересылку писем
- пожать картинки (хранить картинки можно [тут](https://sender.yandex-team.ru/yandex.spravochnik/account/shared-files/))
- проверить, что у всех ссылок есть разный идентификатор, который используется во [wrap](https://wiki.yandex-team.ru/sender/manual/#soderzhanie)
- проверить работоспособность и utm-метки ссылок
