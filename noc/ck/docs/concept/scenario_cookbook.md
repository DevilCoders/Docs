# Сценарный cookbook

## Выполнение команд на устройстве

Для этого используется директива

```yaml
- name: Execute 'some command'
  execute:
    cmd:
    - cmd: some command
```

```yaml
- name: Execute 'some command'
  execute: {cmd: [{cmd: reset bgp all}]}
```

### Выполнить определенные команды в зависимости от вендора
```yaml
- name: Reset BGP Huawei
  when: [hw: Huawei]
  execute: {cmd: [{cmd: reset bgp all}]}
- name: Reset BGP Arista
  when: [hw: Arista]
  execute: {cmd: [{cmd: clear bgp *}]}
```

### Выполнить команду которая требует дополнительного подтверждения

```yaml
- name: Reset startup config
  when: [hw: Huawei]
  execute:
    cmd: [{cmd: reset saved-configuration, timeout: 30}]
    questions: [{q: "The configuration will be erased to reconfigure", a: "Y"}]
```

### Выполнить команду и сохранить вывод в переменную mgmt_vrf

```yaml
- name: Save MGMT vrf name
  execute:
    cmd:
      - cmd: "sudo ip vrf show mgmt | awk '{print $1}'"
        parser: echo
  register: mgmt_vrf
```

### Распарсить вывод команды в словарь

```yaml
- name: Huawei.CE
  when: [hw: Huawei.CE]
  execute: {cmd: [{cmd: display device elabel, parser: vrp_display_elabel}]}
  register: serial
```

```python
    # app/builtin/actions/execute.py
    @staticmethod
    def parse_vrp_display_elabel(data: str) -> Dict[str, str]:
        result: Dict[str, str] = {}
        section = ""
        barcodeline = "BarCode="
        for line in data.split("\n"):
            # Якорь [Board Properties] повторяется
            # и не несет полезной информации
            if line.startswith("[") and not line.startswith("[Board Properties]"):
                section = line.strip()
            elif section == "[Slot_1]" and line.startswith(barcodeline):
                result["serial"] = line[len(barcodeline):].strip()
            return result
```

### Использовать переменную в условии

```yaml
- name: apt-get update in GRT
  execute:
    cmd:
      - cmd: "sudo apt-get update -qq"
        timeout: 120
  when: mgmt_vrf.self != "mgmt"
```

## Вызов аннушки

### Вызвать аннушку для определенных генераторов

```yaml
- name: drain spine
  ann_deploy:
    gens:
      - rpl
      - l3
    no_gens:
      - qos
```

### Вызвать аннушку c определенным filter-acl

```yaml
- name: Deploy BGP
  ann_deploy:
    filter_acl:
      - hw: hw.Huawei
        text: |
          bgp *
            ~ %global
      - hw: hw.Juniper
        text: |
          protocols
            bgp
              ~ %global
```

## Взаимодействие с Racktables

### Добавить теги на устройство

```yaml
- name: add maintenance tags
  racktables_tag:
    state: present
    name:
      - нагрузка снята автоматикой
      - отключен
      - апгрейд или замена
```

### Убрать теги с устройства

```yaml
- name: del maintenance tag
  racktables_tag:
    state: absent
    name:
      - нагрузка снята автоматикой
      - отключен
      - апгрейд или замена
```

## Управление контекстом выполнения

### Прервать выполнение сценария с ошибкой

```yaml
- name: fail if wrong version
  fail:
    msg: "Wrong version after installation!"
  when: mondata_version_after.self != job_vars.mondata_version
```

### Сделать паузу в выполнении

```yaml
- name: wait for 30 seconds before check the log file
  sleep:
    duration: 30
```

### Выполнить action только для Huawei

```yaml
- name: Reset BGP Huawei
  when: [hw: Huawei]
  execute: {cmd: [{cmd: reset bgp all}]}
```
Еще примеры фильтров по hw, полный список в [nocdev/annushka](https://noc-gitlab.yandex-team.ru/nocdev/annushka/-/blob/master/netdev/data/devdb.json)
```
Huawei.CE
Cisco.Nexus
Arista.A7050
PC.Whitebox.Mellanox
Cisco.Catalyst.C2900.C2960.C2960X
```

### Параметры для сценария

#### Простые параметры трех типов `bool/int/str`
```yaml
name: scenario_name
job_vars:
    - name: bool_param
      type: bool
    - name: int_param
      type: int
    - name: str_param
      type: str
actions:
  - name: Выполняется только если job_vars.bool_param == true
    debug:
      msg: "YES"
    when: job_vars.bool_param

  - name: Спим int_param секунд
    sleep:
      duration: "{{ job_vars.int_param }}"
    when: job_vars.int_param > 10

  - name: Вылняем команду в str_param
    execute:
      cmd:
        - {cmd: "{{ job_vars.str_param }}"}
    when: job_vars.str_param != ""
```

#### Списки параметров `many_values: true`
```yaml
name: scenario_name
job_vars:
    - name: list_str_param
      type: str
      many_values: true
actions:
  - name: Удаляем все файлы из списка list_str_param
    execute:
      cmd:
        - {cmd: "rm {{ job_vars.list_str_param|join(' ') }}"}
```

#### Значения по умолчанию `default: ...`
```yaml
name: scenario_name
job_vars:
    - name: metric
      type: int
      default: 100

    - name: list_ips
      type: str
      many_values: true
      default:
        - "1.1.1.1"
        - "2.2.2.2"
actions: []
```

#### Выбор из заранее заданных значений, которые в интерфейсе покажутся в выпадайке:
```yaml
name: scenario_name
job_vars:
  - name: count
    type: int
    many_values: true
    choices: [100, 500, 100500]
    default: [100, 500]
  - name: channel_type
    type: str
    choices: [ "LAB1-VLA", "LAB2-VLA", "VLA-M9", "VLA-STD",
               "SAS-VLA", "SAS-M9", "SAS-STD", "MYT-M9",
               "MYT-STD", "IVA-M9", "IVA-STD"]
```

## Автоматизация согласования через NOCRFCS

```yaml
name: nocrfcs-demo
actions:

  - name: Создаём тикет в NOCRFCS-очереди
    startrek_issue:
      # Указываем очередь в Startrek
      queue: NOCRFCS
      # Выбираем один из шаблонов: сейчас поддерживаются nocrfcs и common
      template: nocrfcs
      # Указываем тип тикета: задача
      issue_type_key: task
      # Указываем контекст для рендеринга тикета по выбранному
      context:
        name: Снятие трафика с линка man1-x2 100ge5/0/3 - man-36d8 e32/1
        change_type: Normal
        responsible: ekulemzin
        infra: NOC DC - Core
        datacenters:
          - ДЦ MAN
        previous_experience: Был опыт и он был успешным
        is_automated: false
        change_testing: Не тестировалось
        service_impact: Нет
        start: "2021-07-25T01:19:00+03:00"
        end: "2021-07-25T01:29:00+03:00"
        description: |-
            %%(diff)Diff for man1-x2:
            interface 100GE5/0/3
            + description man-36d8 e32/1 damaged
            -   eth-trunk 368
            -   portswitch
            %%
        execution: |-
            Patch for man1-x2:
            interface 100GE5/0/3
             description man-36d8 e32/1 damaged
                undo eth-trunk
                undo portswitch
        rollback: Не предусмотрено
    # указываем имя переменной, в которую запишется результат; далее можно будет обращаться к
    # переменным: {{ my_issue.key }}
    register: my_issue

  - name: Ждём согласования NOCRFCS-тикета
    wait_for_issue_status:
      issue: {{ startrek_issue }}  # тут подставится тот тикет, с которым была создана джоба
      statuses:
        - pending  # ждём перехода тикета в статус "В ожидании" (pending)

  - name: Нажимаем "Начать выполнение" у NOCRFCS-тикета
    startrek_transition_execute:
      issue: {{ startrek_issue }}  # тут подставится тот тикет, с которым была создана джоба
      transition: inProgress  # аналогично нажатию кнопки "Начать выполнение"

  # ... проводим работы ...

  - name: Закрываем NOCRFCS-тикет с успешным статусом
    startrek_transition_execute:
      issue: "{{ my_issue.key }}"
      transition: close  # аналогично нажатию кнопки "Закрыть"
```

Подробнее можно прочитать на страницах с описанием Action-ов:

- [{#T}](../plugins/startrek_issue_action.md)
- [{#T}](../plugins/startrek_transition_execute_action.md)
- [{#T}](../plugins/wait_for_issue_status_action.md)
