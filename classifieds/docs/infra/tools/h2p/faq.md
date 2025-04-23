# FAQ

#### **Q: IDE от JetBrains (DataGrip, GoLand, PyCharm) ругается на ipv4**

**A:** Проверьте поддержку `IPv6` в IDE (по умолчанию - **выключена**). [Как включить](https://nda.ya.ru/t/1uNCk3wn3VxVTJ)

------

#### **Q: IDE от JetBrains (DataGrip, GoLand, PyCharm) ругается на timezone (`serverTimezone`)**

**A:** Установите в настройках своей IDE таймзону `UTC` (или другую, какую вам нужно)

Например, в **DataGrip** настройка называется `serverTimezone` на вкладке `Advanced` при создании нового подключения.

------

#### **Q: `Connection timed out` при подключении к `h2p.vertis.yandex.net`/`h2p.test.vertis.yandex.net`**

**A:** Похоже, что нет дырки в `Puncher`. Сделайте тикет в [VASUP](https://st.yandex-team.ru/createTicket?queue=VASUP&_form=63062).

------

#### **Q: Error: can't get available ssh keys from SSH agent**

**A:** Проверьте:
* что SSH ключ добавлен в `ssh-agent`:

  `ssh-add -l`

  Если ничего не выводится, то добавить ключ можно командой: `ssh-add -K ~/.ssh/id_rsa`
* что среди ключей в `ssh-agent` есть ключ, который привязан к Стаффу и он имеет тип `RSA`
* что имя пользователя в системе совпадает с логином на Стаффе

  Узнать имя пользователя в системе:

  `whoami`
* что стоит правильное время в системе

------

#### **Q: administratively prohibited: port forwarding is disabled**

**A:** Проверьте, что вы запросили доступ в этот сервис через IDM и вам его подтвердили. Это можно посмотреть в самом IDM.

Проверьте, что указали правильный адрес сервиса.

------

#### **Q: Проблема не попадает ни под один пункт выше**

**A:** Создавайте тикет в [VASUP](https://st.yandex-team.ru/createTicket?queue=VASUP&_form=63062)



