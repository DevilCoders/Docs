# Блокировка syn-флуда на балансерах

Если к вам обращаются коллеги из других подразделений, например, из дежсмены поиска, и начинают сообщать о DDoS на yandex.ru, то стоит проверить атаку на syn-flood.

Некоторые вариации DDoS, в частности syn-flood или даже попытки положить сервис вполне реальными запросами от ботнета, можно поблочить на уровне балансеров.

**Как это делать?**

Сначала проверяем гипотезу о син-флуде. (Параллельно неплохо бы отыскать любого из [neverov@](https://staff.yandex-team.ru/neverov), [ezhichek@]((https://staff.yandex-team.ru/ezhichek)) и передать поступившую жалобу - но и самостоятельно немного поспасать сервис тоже полезно).

Простой способ - поискать его на графиках. Работает, если флуд продолжается достаточно долго, чтоб в cacti появилась очередная точка.
Ищем в двух местах - графики пакет-рейта и трафика на портах и графики cps/pps/трафика для сервиса.
Для yandex.ru смотрим балансеры в racktables со страницы сервиса - [VSG yandex.ru](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=957)
Выбираем балансер [например - sas1-2lb6b](https://racktables.yandex-team.ru/index.php?page=object&object_id=2801) и с "ports and links" переходим на графики в cacti (красные стрелки на скриншоте):

![](./_images/img.png)

Попадаем на [графики pps и трафика так, как их видит балансер](http://cacti-noc.yandex.net/graph_view.php?action=tree&tree_id=4&leaf_id=5491802&filter_title=eth1)

Дополнительно смотрим то же самое со стороны коммутатора - переходим на страницу устройства по ссылке (синяя стрелка на предыдущем скриншоте), видим картинку с подсвеченным портом:

![](./_images/img_1.png)

Далее (по красным стрелкам) на графики [порта коммутатора](http://cacti-noc.yandex.net/graph_view.php?action=tree&tree_id=3&leaf_id=5480996&filter_title=100ge1%2F0%2F3%3A4)

Для случая syn-флуда (если он продолжается уже достаточное для отрисовки очередной точки), на графиках будет существенный рост pps при незначительном росте по трафику.

Параллельно нужно смотреть сервисные графики в [cacti](http://cacti-noc.yandex.net) - ветка Balancers -> Agg - Connections/Svc Traffic/Svc Packets
Ищем через FQDN сервиса, для yandex.ru поисковая строка - `^yandex.ru`
Наблюдаемый эффект должен быть сходным - заметный рост pps и cps при небольшом росте трафика. На скриншоте картинка по cps, характерная как раз для syn-flood.

![](./_images/img_2.png)

Альтернатива (или дополнение) графикам - tcpdump. Он же необходим для следующего шага ~~в борьбе за светлое будущее во имя луны~~.
Приходим по ssh на балансер и запускаем его, любимого (с правами root, конечно же) с фильтрами по dst на yandex.ru - посмотреть соотношение пакетов в потоке входящего трафика на сервис.
При обычной нагрузке днем сто тысяч син-пакетов на yandex.ru (дополнительный фильтр с флагом) набегают за 6-8 секунд:
```
root@sas1-2lb6b:/home/neverov# time tcpdump -c 100000 -pni eth1 'tcp[13] == 2' and '(dst net 77.88.55.0/24 or dst net 5.255.255.0/24)' > /dev/null
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), capture size 262144 bytes
100000 packets captured
101151 packets received by filter
271 packets dropped by kernel

real    0m7.837s
user    0m0.890s
sys     0m0.270s
```

При этом весь поток пакетов заметно больше (запуск без фильтра по типу пакетов, только dst net)
```
root@sas1-2lb6b:/home/neverov# time tcpdump -c 100000 -pni eth1 '(dst net 77.88.55.0/24 or dst net 5.255.255.0/24)' > /dev/null
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), capture size 262144 bytes
100157 packets captured
229756 packets received by filter
125672 packets dropped by kernel

real    0m0.800s
user    0m0.526s
sys     0m0.137s
```

Если видим, что соотношение перетянуто в пользу syn-пакетов - запускаем адское комбо
```
root@sas1-2lb6b:/home/neverov# tcpdump -c 100000 -pni eth1 '(dst net 77.88.55.0/24 or dst net 5.255.255.0/24)' | awk '{ print $3 }' |  cut -d "." -f 1-4 | sort | uniq -c | sort -n | tail -50
```
и смотрим вывод - это подсчет чиста syn-пакетов с сорс-адреса в 100000 штук. Обычно выглядит как-то так
```
     55 31.173.85.62
     55 93.125.6.160
     56 37.78.12.60
     58 159.89.19.98
     64 165.227.129.208
     64 165.227.174.113
     64 212.100.146.17
     73 159.89.18.123
     73 46.39.53.186
     73 81.24.131.93
     74 176.112.220.4
     82 46.101.107.203
    102 93.185.30.253
    135 176.110.124.74
    232 46.61.152.186
    304 94.142.141.116
```
Лидируют NAT-ы (нужно смотреть PTR и whois) и довольно гладкое распределение далее. Заметные - в 10-100 и более раз лидеры - кандидаты на блокировку. В принципе полезно посмотреть несколько сотен пакетов с лидирующих source-адресов глазами - действительно ли это только syn-ы, или вполне полноценные сессии. Попробовать поискать общие признаки, позволяющие такой поток дешево фильтровать (например - у всех пакетов одинаковый src_port).
Когда syn-ов летит много - можно смотреть лидеров в миллионе пакетов.

Далее переходим непосредственно к фильтрации. Фильтровать вредный поток нужно сразу на входе, минимально нагружая фаервол - т.е. в mangle prerouting. И не плодить десятки-сотни правил, а использовать ipset.
Создаем ipset для хранения врагов
```
root@sas1-2lb6b:/home/neverov# ipset create enemy_v4 family inet
```
и правило фильтрации (не заморачиваясь с деталами - баним src)
```
root@sas1-2lb6b:/home/neverov# iptables -t mangle -I PREROUTING -m set --match-set enemy_v4 src -j DROP
```
ну а далее просто закидываем адреса врагов в сет
```
root@sas1-2lb6b:/home/neverov# ipset add enemy_v4 $ip_address
```
с использованием любых удобных баш-оптимизаций.
Если внезапно хотим кого-то конкретного разбанить - то
```
root@sas1-2lb6b:/home/neverov# ipset del enemy_v4 $ip_address
```
Всех разбанить, сохранив возможность быстро закинуть врагов назад в блокировку
```
root@sas1-2lb6b:/home/neverov# ipset flush enemy_v4 $ip_address
```
Блокировать, конечно же, нужно на всех балансерах сервиса - и именно здесь вам пригодятся любимые баш-оптимизации ;)

------
[Первоисточник статьи](https://wiki.yandex-team.ru/NOC/block-syn-on-l3/)
