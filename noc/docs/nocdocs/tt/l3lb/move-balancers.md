# Перенос балансировщика
На основе тикета https://st.yandex-team.ru/TRAFFIC-12781

# Мотивация
Иногда бывает что нужно перераспределить нагрузку на балансировщиках.

Допустим, у нас есть балансировщики, которые смотрят в те же коммутаторы что неоптимально с точки зрения отказоустойчивости и распределения нагрузки:

```
myt-lb11a
  myt-a1d	100ge1/0/41:1
  myt-a1c	100ge1/0/41:1
myt-lb11b
  myt-a1d	100ge1/0/42:1
  myt-a1c	100ge1/0/42:1
```
и
```
myt-3lb51a
  myt-a1a	100ge1/0/38:3
  myt-a1b	100ge1/0/38:3
myt-3lb51b
  myt-a1a	100ge1/0/42:1
  myt-a1b	100ge1/0/42:1
```

Тогда нам хотелось бы привести балансировщики к конфигурации:
```
myt-3lb51a
  myt-a1a	100ge1/0/38:3
  myt-a1b	100ge1/0/38:3
myt-lb11b > myt-3lb51b (rename)
  myt-a1d	100ge1/0/42:1
  myt-a1c	100ge1/0/42:1
```
и
```
myt-lb11a
  myt-a1d	100ge1/0/41:1
  myt-a1c	100ge1/0/41:1
myt-3lb51b > myt-lb11b (rename)
  myt-a1a	100ge1/0/42:1
  myt-a1b	100ge1/0/42:1
```


# Алгоритм проведения работ
0. Подготовка - записываем IP адреса балансировщиков чтобы во время переноса пользоваться IP адресами.
1. Меняем местами балансировщки через CLI в источнике истины - Racktables.
    ```
    cd $ARCADIA
    cd arc/noc/traffic/tools/swap-lbs
    python3 ./cli.py myt-3lb51b.yndx.net myt-lb11b.yndx.net    
    ```
2. Меняем настройки балансировщиков и переименовываем хосты, указывая в `-n` новое имя хоста на обоих хостах переезжающей пары
    ```
    # Заходим на хост по сохранённому IP адресу.
    ssh 5.255.219.249 # ssh 87.250.241.225
    # обнуляем конфигурацию keepalived чтобы во время переименования не случилось несчастья
    truncate -s0 /etc/keepalived/keepalived.conf
    # переименовываем хост и качаем его настройки
    /opt/balancers/scripts/update-configs.py -n myt-3lb51b.yndx.net # /opt/balancers/scripts/update-configs.py -n myt-lb11b.yndx.net
    # убираем анонсы
    sudo birdc disable direct12 ; sudo birdc disable direct13 ; sudo birdc disable direct14 ; sudo birdc disable direct15 ; sudo birdc disable direct100 ; sudo birdc6 disable direct12 ; sudo birdc6 disable direct13 ; sudo birdc6 disable direct14 ; sudo birdc6 disable direct15 ; sudo birdc6 disable direct100
    ```
    Нажать метлу [Clear entry from known_hosts] Clear known_hosts в racktables.
3. *Синхронно* рестартуем серверы `reboot`
4. После рестарта
    
    * Генерируем конфиги `natasha`
    ```
    ANSIBLE_HOST_KEY_CHECKING=False l3-do -e 'sudo natasha-gogo oneshot' -l myt-lb11b.yndx.net myt-3lb51b.yndx.net    
    ```
    * Идём в racktables/l3manager  и передеплоиваем сервисы. Для l3manager-а: идём в https://l3.tt.yandex-team.ru/balancer , ищем myt-lb11b.yndx.net и деплоим.
    * Проверяем анонсы сервисов
    * Рестартуем  firewall
    ```
    ANSIBLE_HOST_KEY_CHECKING=False l3-do -e 'sudo make -C /usr/local/balancers/iptables install-tarball' -th 10 -l myt-lb11b.yndx.net myt-3lb51b.yndx.net
    ```
5. Переназначем хосты в bot.yandex-team.ru
