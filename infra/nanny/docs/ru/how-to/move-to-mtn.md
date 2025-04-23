# Перевод сервиса на MTN

##  О чём {#dislaimer}

Попробуем в этом документе собрать инструкцию по переводу сервиса на отдельную от хоста сеть (a.k.a MTN).

{% note warning %}

Для перевода MTN сервис должен использовать изоляцию по файловой системе. Для этого воспользоваться инструкцией [Перевод сервиса на отдельный mount namespace](storage/move-to-rootfs.md).

{% endnote %}

##  Gencfg {#gencfg}
Все группы в Gencfg готовы к включению MTN (т.е. генерируются IP адреса, резервируются project id и т.д.). Если в следующих пунктах возникли проблемы при выкладке - необходимо **выбрать наиболее свежий тэг** Gencfg.

Хочется отметить важные моменты:
* Группы gencfg **нельзя переименовывать**
Т.к. название группы участвует в DNS именах контейнеров. При смене названия группы сменятся:
* DNS и IP адреса контейнеров, а так же hostname - старые через какое-то время пропадут из DNS

##  Nanny {#nanny}
Для включения MTN необходимо на вкладке `Instances`:

* Выставить галку `Isolate instance network (use MTN)`.

    ![img](https://jing.yandex-team.ru/files/sshipkov/mtninstances.0178b17.png)

* Сохранить изменения `Runtime Attrs` с помощью нажатия кнопки `Save`.

Далее необходимо проверить, что сервис gencfg для всех инстансов заполнил необходимые для работы в MTN поля. Для этого мы запускаем команду на подготовку ревизии в ISS, выбрав `Present in CMS/ISS only` для нужной ревизии.

![img](https://jing.yandex-team.ru/files/sshipkov/2018-01-0916-15-36.d18c5f3.png)

![img](https://jing.yandex-team.ru/files/sshipkov/2018-01-0916-16-21.ec0558f.png)

В случае проблем эта процедура буде завершаться с ошибкой: `"Use MTN" flag is set in snapshot but no network interfaces given in gencfg group`. В этой ситуации необходимо обращаться в gencfg-support чат.

##  Firewall {#firewall}

* Несмотря на то, что входящие соединения можно принимать через хостовый (`dom0`) сетевой интерфейс и адрес, исходящие соединения будут осуществляться с нового IP адреса, поэтому необходимо настроить приёмники наших соединений.
* Доступы к passport и другим сервисам с отдельной авторизацией может пропасть после переезда в MTN, его надо заказывать отдельно.
* На данный момент макросы групп входят в макрос `_SEARCHPRODNETS_` и доступы через FW не пропадут.
Это поведение может измениться: [https://st.yandex-team.ru/RX-123](https://st.yandex-team.ru/RX-123)

##  Мониторинг YASM (голован) {#yasm}

Если вы мониторитесь через [unistat](https://wiki.yandex-team.ru/golovan/stat-handle/unistat-setup/)-ручку, нужно включить в сервисе флажок `Don't start subagent but bind its directory into container filesystem`. Этого можно будет не делать после закрытия тикета [https://st.yandex-team.ru/GOLOVAN-5257](https://st.yandex-team.ru/GOLOVAN-5257)
Подробнее: [https://wiki.yandex-team.ru/golovan/yasmagent/subagent/](https://wiki.yandex-team.ru/golovan/yasmagent/subagent/)

![img](https://jing.yandex-team.ru/files/sshipkov/2017-12-2700-15-02.451a156.png)

##  NAT scheme {#nat-scheme}
При запуске инстанса демон yandex-hbf-agent получает список контейнеров, запущенных с изоляцией по сети и настраивает правила DNAT, так, что все входящие соединения на порт, выделенный в GENCFG направляются в контейнер. Таким образом все клиенты могут продолжать пользоваться старым адресом сервиса (например, при миграции на MTN сеть).

Однако схема с NAT является временной. Поэтому после окончательного переезда в MTN необходимо переконфигурировать сервисы и балансеры, которые ходят в инстансы вашего сервиса.

###  Коммунальный балансер {#common-balancer}
Если ваш сервис живёт за коммунальным балансером, то **после переезда в MTN** в его секции нужно включить флажок `Use MTN`:

![img](https://jing.yandex-team.ru/files/sshipkov/2017-12-2700-24-55.240a548.png)

###  AWACS {#awacs}
Если в ваш сервис ходит балансер, поднятый через AWACS, то **после переезда на MTN** в его AWACS backends необходимо включить флажок `Use MTN`:

![img](https://jing.yandex-team.ru/files/sshipkov/2017-12-2700-20-41.f0aadf6.png)

###  Отключение NAT схемы для сервиса {#service-dbf-nat}
Прямо сейчас можно отключить NAT для конкретного сервиса **после переезда на MTN**. Для этого нужно в разделе `Instances` выбрать опцию `DISABLED` в поле `ENABLE_HBF_NAT`

![img](https://jing.yandex-team.ru/files/sshipkov/disablehbfnat.fb14367.png)

