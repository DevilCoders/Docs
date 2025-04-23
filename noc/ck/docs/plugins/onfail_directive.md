# onfail - выполнить произвольную логику после ошибки

В данную директиву можно указать произвольный набор шагов. В случае любой ошибки внутри шага или блока, `onfail` будет выполнен. Если ошибки не было, `onfail` будет проигнорирован.

Может использоваться в любых шагах (так же как и when). 

Пример: проверяем доступность точки, и постим сообщение о ошибке в тикет, если она не доступна, после чего останавливаем выполнения сценария.


```yaml
  - name: test_ping
    execute:
      cmd:
        - cmd: "ping -c1 {{ hostname }} >/dev/null&& echo OK||echo NOK"
          parser: echo
          timeout: 30
      hosts:
        - noc-sas.yandex.net
    register: chk
    onfail:
      - name: check trouble
        startrek_comment:
          issue: "{{ startrek_issue }}"
          text: |-
            Проблемы в момент проверки доступности точки
          summonees: "{{ nocduty }}"
```

Объяснение порядка вызова `onfail` такое – если в сценарии написано:

```yaml
- call: my_callback1
  onfail:
    - call: my_rollback1
    - call: my_rollback2
- call: my_callback2
```

, то это будет аналогично псевдокоду:

```yaml
try:
    my_callback1()
except:
    my_rollback1()
    my_rollback2()
    raise
my_callback2()
```
