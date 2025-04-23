# Призыв дежурных NOC в сценарий из Warden

Призывает текущих дежурных NOC из Warden 
https://noc.hot-desk.hd.yandex-team.ru/

Использование:

```
  - name: Summon
    warden_nocduty:
    register: nocduty

  - startrek_comment:
        issue: "{{ startrek_issue }}"
        summonees: "{{ nocduty }}"
        text: bla-bla-bla
```
