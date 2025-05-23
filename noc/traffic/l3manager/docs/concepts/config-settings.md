# Настройка виртуального сервера

Виртуальные серверы в L3 manager имеют следующие группы настроек:

## VS Definition {#section_vxt_rlf_sfb}

Основные настройки виртуального сервера. На скриншоте приведены значения по умолчанию:

![image](../_assets/new-vs1-vsdef.png =600x175)

- **Get new IP** — тип адреса, который будет назначен вашему серверу:
    
    - Internal IPv4 — IPv4 адрес для внутренних сервисов.
    - Internal IPv6 — IPv6 адрес для внутренних сервисов.
    - External IPv4 — IPv4 адрес для внешних сервисов.
    - External IPv6 — IPv6 адрес для внешних сервисов.
    
    Внешний сервис — это сервис, к которому будут подключаться из внешней сети. Примеры внешних сервисов:
    
    - Главная страница Яндекса.
    - Сервисы, к которым будут подключаться outsource-сотрудники, не имеющие доступа к VPN.
    - Все проекты клиентов Яндекс.Облака.
    
    На данном этапе необходимо выбрать только тип адреса. L3 manager самостоятельно выдаст и подставит конкретное значение IP-адреса в поле **IP**.
    
- **Port** — порт вашего приложения, на который будут отправляться запросы пользователей. {#port}
- **Protocol** — протокол подключения к вашему сервису: TCP, UDP или FWM (Firewall mark). Если вы хотите использовать протокол FWM, проконсультируйтесь с [командой L3](mailto:slb@yandex-team.ru).

## RS check settings {#section_odv_rlf_sfb}

Настройки для [проверки активности рилов](checks.md#rs-checks). На скриншоте приведены значения по умолчанию:

![image](../_assets/new-vs2-rscheck.png =600x205)

- **CHECK_TYPE** — метод, который L3 manager будет использовать для отправки запросов к вашему приложению. Возможные значения:
    - HTTP_GET.
    - SSL_GET. При данном запросе не происходит проверка корректности сертификата. L3 manager проверяет только успешность SSL-handshake.
    - TCP_CHECK.
    
    {% note info %}
    
    L3 Балансер не закрывает соединения пакетов с [флагом](https://www.keycdn.com/support/tcp-flags) FIN, открытые при проверке доступности. Вместо этого используются пакеты в флагом RST.
    
    {% endnote %}
    
- **CONNECT_PORT** — порт, на который L3 manager будет отправлять проверочные запросы.
- **HOST** — значение заголовка Host при использовании методов HTTP_GET и SSL_GET.
- **CHECK_URL** — url, на который L3 manager будет отправлять проверочные запросы. {#check-url}
- **CHECK_RESULT** — ответ приложения, при котором рил будет считаться доступным: {#check-result}
    - STATUS_CODE — проверка по коду статуса. В поле указывается код корректного ответа вашего приложения, например — 200.
    - DIGEST — проверка по дайджесту ответа. В поле указывается значение дайджеста, которое должно совпадать с md5-суммой тела ответа.
    
    Проверки по коду статуса и дайджесту ответа могут осуществляться одновременно.
    

## Advanced settings {#section_otv_rlf_sfb}

Дополнительные настройки для распределения трафика между рилами. На скриншоте приведены значения по умолчанию:

![image](../_assets/new-vs3-adsett.png =600x295)

- **SCHEDULER** — алгоритм балансировки: {#ul_wxl_ylf_sfb}
    - wrr — [Weighted Round-Robin](http://kb.linuxvirtualserver.org/wiki/Weighted_Round-Robin_Scheduling). Новые сессии распределяются по рилам поочередно, без учета текущего трафика, но с учетом веса рилов.
    
    - wlc — [Weighted Least-Connection](http://kb.linuxvirtualserver.org/wiki/Weighted_Least-Connection_Scheduling). Алгоритм приоритезирует рилы с меньшим количеством сессий. При появлении в конфигурации нового рила, весь новый трафик будет перенаправляться на него, пока количество сессий на всех рилах не уравновесится.
    
    Счетчик количества сессий может запаздывать относительно действительного количества соединений. Это означает, что новый рил может временно оказаться перегруженным, после чего алгоритм перерассчитает количество соединений и выправит распределение трафика.
    
- **ANNOUNCE** — признак того, что доступность этого виртуального сервера влияет на анонс его IP-адреса. Возможные значения:
    
    - true — Если данный виртуальный сервер неактивен, то IP-адрес сервиса перестает анонсироваться при недоступности рилов для данного виртуального сервера. Для того, чтобы IP-адрес начал анонсироваться, необходимо, чтобы за всеми виртуальными серверами с этим адресом, у которых `ANNOUNCE: true`, были доступные рилы и выполнялось условие набора QUORUM и HYSTERESIS (о них следующий пункт);
    - false — Вне зависимости от состояния рилов данного виртуального сервера, он не будет влиять на логику анонсирования указанного IP-адреса сервиса.
    
- **QUORUM** и **HYSTERESIS** — параметры, определяющие логику активности виртуального сервера:
    
    - Виртуальный сервер активен, если общий вес работающих рилов больше или равен значению (QUORUM + HYSTERESIS).
    - Виртуальный сервер неактивен, если общий вес работающих рилов меньше значения (QUORUM - HYSTERESIS).
    
    Значения QUORUM и HYSTERESIS представлены в конфигурации keepalived как целые числа. Если в описании сервиса эти значения указаны в процентах, то в момент генерации конфигурации они вычисляются, основываясь на указанных статических весах рилов (если вес рила специально не указан, его значение по умолчанию — 1).
    
    {% note alert %}
    
    Если указанное пользователем значение параметра QUORUM или HYSTERESIS превышает сумму статических весов всех рилов для данного балансера, то значение параметра устанавливается равным этой сумме (с учетом DC_FILTER флага).
    
    {% endnote %}
    
    {% note info %}
    
    [Флапающие рилы](terms.md#flapping-reel) могут приводить к нестабильной работе всего виртуального сервера. Установите такие значения параметров, при которых значение (Q - H) меньше, но не равно значению (Q + H). В этом случае флапающий рил не будет изменять логику анонса. При этом максимальные значения Q и H не могут превышать суммарный статический вес рилов с учетом DC_FILTER.
    
    {% endnote %}
    

- **DYNAMICWEIGHT** — признак использования [динамического веса рилов](checks.md#weigths). {#dinamicweight}
    - true — динамические веса.
    - false — статические веса.
    
    {% note info %}
    
    После включения динамических весов на каждой итерации цикла проверки с полученными ранее целочисленными значениями QUORUM и HYSTERESIS будет сравниваться _текущий_ суммарный вес рилов.
    
    {% endnote %}
    
- **WEIGHT_IN_HEADER** — способ передачи динамических весов: {#weight-in-header}
    - true — передавайте вес в заголовке `RS-Weight: <новый вес рила>`.
    - false — передавайте вес в теле ответа `rs_weight = <новый вес рила>`.
    
    По умолчанию вес рила не может быть равен 0. Если вам необходимо задавать такой вес, используйте настройку [WEIGHT_ALLOW_ZERO](#weight-allow-zero). Если вы хотите полностью убрать трафик с рила, необходимо перестать отвечать на [проверку статуса](#section_odv_rlf_sfb).
    
- **WEIGHT_RATIO** — коэффициент, применяемый к полученным от рилов весам. То есть на сколько процентов от текущего веса может измениться вес рила за одну итерацию. Минимальный шаг при изменении — 1.
    
    Настройка позволяет изменять вес рилов более плавно. Например, для рила с изначальным весом 100, желаемым весом 40 и коэффициентом 30 на каждом шаге вес будет изменяться максимум на 30 процентов: 100, 67, 44, 40.
    
- **WEIGHT_ALLOW_ZERO** — признак того, что рилам может быть задан вес 0. {#weight-allow-zero}
    - true — Рил с весом 0 будет считаться активным, но не будет получать новых пользовательских сессий. Пользовательские сессии с данным рилом продолжат существовать до завершения сессии или наступления timeout.
    
    Исключение — виртуальные серверы с включенной настройкой [PERSISTENT_TIMEOUT](#persistent-timeout). Такие серверы продолжат получать новые соединения от IP-адресов клиентов при уже существующих сессиях с этих адресов.
    
    - false — L3 manager не будет изменять вес рила при получении веса 0.
    

## DC settings {#section_vrw_rlf_sfb}

Настройки датацентров. На скриншоте приведены значения по умолчанию:

![image](../_assets/new-vs4-dcsett.png =600x207)

- **Load balancers** — Вес датацентров, учитываемый при распределении пользовательского трафика согласно [BGP](https://en.wikipedia.org/wiki/Border_Gateway_Protocol) (датацентры с большим весом пессимизированы).
  
    {% note alert %}
    
    Если вам необходимо изменить данную настройку, проконсультируйтесь с [командой L3](mailto:slb@yandex-team.ru).
    
    {% endnote %}
    
    {% note info %}
    
    Анонсы сервисов из ДЦ MAN искусственно пессимизируются для Московских пользователей и датацентров. Это позволяет не увеличивать задержки в ответах пользователю.
    
    {% endnote %}
  
- **DC_FILTER** — признак того, что L3 балансеру доступны рилы только в своем датацентре. Логика актуальна только для московских ДЦ:
    - true — балансеру в одном из московских ДЦ доступны только рилы этого ДЦ.
    - false — балансеру в одном из московских ДЦ доступны рилы во всех московских ДЦ (Ивантеевка, Сасово, Мытищи).
    
- **INHIBIT_ON_FAILURE** — признак того, что рилы, не прошедшие проверку доступности, будут иметь вес 0. Возможные значения:
    - true — рил, не прошедший проверку доступности, получает вес 0.
    - false — рил, не прошедший проверку доступности, будет считаться недоступным.
    
- **PERSISTENT_TIMEOUT** — скрытая настройка. Количество секунд, при которых пользователь с одного IP-адреса будет автоматически перенаправляться на рил, с которым он уже установил успешное соединение, вне зависимости от статуса рила. {#persistent-timeout}

    {% note alert %}
    
    Перед изменением настроек **INHIBIT_ON_FAILURE** и **PERSISTENT_TIMEOUT** проконсультируйтесь с [командой L3](mailto:slb@yandex-team.ru).
    
    {% endnote %}
    

## RS settings {#section_lkx_rlf_sfb}

Список рилов:

![image](../_assets/new-vs5-rssett.png =600x132)

Рилы могут быть заданы списком адресов, группами Кондуктора, Gencfg или RT.

Примеры списка рилов:

{% list tabs %}

- Адреса рилов

  Адреса могут быть указаны в формате `<адрес_рила>` или `<адрес_рила> weight=<статический вес рила>`. Вес рила по умолчанию — 1.

  ```
  backend1.yandex.net weight=5
  backend2.yandex.net weight=1
  backend3.yandex.net weight=4
  ```

- Conductor

  ```
  %conductor_group_1
  %conductor_group_2
  ```

- Gencfg

  ```
  @GENCFG_VLA_GROUP
  @GENCFG_SAS_GROUP
  ```

- RT

  ```
  $market_test_rs
  ```

{% endlist %}