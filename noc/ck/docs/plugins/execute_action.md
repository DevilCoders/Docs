# execute - выполнить команду на устройстве

Выполнить произвольную команду на устройстве, сохранив если нужно вывод. Вывод можно распарсить произвольной логикой указав ее в аргументе `parser: whatever` и поместив в метод `parse_whatever`: https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/blob/master/app/builtin/actions/execute.py. 

Пример: если устройство Ариста - выполняем на ней команду `write erase` и отвечаем на промпт.

```yaml
- name: Arista reset
  when: [hw: Arista]
  execute:
    cmd: [{cmd: 'write erase'}]
    questions: [{q: "Proceed with erasing startup configuration.+", a: "y"}]
```

Пример: выполняем на устройстве команду `sudo mlxfwmanager | grep FW | grep -v Running | awk '{print $2}'` и сохраняем вывод в переменную fw_after_upgrade.

```yaml
- name: collect FW after upgrade
  execute:
    cmd:
      - cmd: sudo mlxfwmanager | grep FW | grep -v Running | awk '{print $2}'
        timeout: 30
  register: fw_after_upgrade
```


Пример: парсим длинный вывод методом `app.builtin.actions.execute.Exec.huawei_serial` и сохраняем в переменной `serial`.


```yaml
- name: Huawei_8800
  when: [hw: Huawei.CE.CE8800]
  execute: {cmd: [{cmd: 'screen-length 0 temporary'}, {cmd: 'display device esn', parser: huawei_serial}]}
  register: serial
```


Пример: обрабатываем ошибки, встреченные по ходу выполнения экшена.

```yaml
- name: ждать, пока тикет не закроется или не настанет таймаут
  wait_for_issue_status:
    issue: "{{ startrek_issue }}"
    statuses:
        - closed
    timeout: "{{ job_vars.duration }}"
    onfail:
        - name: отписать в тикет об удалении мьюта
          startrek_comment:
            issue: "{{ startrek_issue }}"
            text: >-
                ЦК не смог дождаться закрытия тикета, созданный мьют в juggler будет удалён:
                https://juggler.yandex-team.ru/mutes/?query=mute_id={{ mute.id }}
```

За объяснением порядка выполнения `onfail` см. [{#T}](./ann_deploy_action.md)

