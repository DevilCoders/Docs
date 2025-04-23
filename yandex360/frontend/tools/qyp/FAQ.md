# FAQ
*устарел*

**Q:** Не работает автодеплой в WebStorm!<br>
**A:** Есть два варианта решения проблемы (нажмите для раскрытия нужного пункта):

<details>
<summary>1. Заставить WebStorm правильно работать с ipv6</summary>
В WebStorm (Cmd + Shift + A => Edit Custom VM)

```
-Djava.net.preferIPv4Stack=false
-Djava.net.preferIPv6Addresses=true
```

После установки данных параметров необходимо перезапустить WebStorm для их применения.

Этот вариант не всегда работает.
(у @ekhurtina все заработало по крайней мере с первого раза, пример конфигурации https://jing.yandex-team.ru/files/ekhurtina/webstorm_qyp_conf.png)
Не забыть в конфигурации указать / в deployment path https://jing.yandex-team.ru/files/ekhurtina/1111111.png

</details>

<details>
<summary>2. Поднять локальный haproxy и продолжить пользоваться ipv4</summary>

```
make qyp-sftp-proxy
make qyp-sftp-proxy [<port=30022> [<host-prefix=$USER>]]
make qyp-sftp-proxy 30021 maya
```

Этот вариант работает всегда, но нужно запускать прокси при рестарте компьютера.
</details>

**Q:** Хочу открыть дев-тачку по адресу mail.yandex.TLD<br>
**A:** В nginx тащится внутренний сертификат для всех mail.yandex.TLD. Достаточно прописать в свой `/etc/hosts` ipv6 адрес своей машинки. Есть ограничение — проект должен находиться в `~/www` (`~/frontend` не сработает).

**Q:** Ничего не работает!<br>
**A:** Обратитесь к @lynn =)
