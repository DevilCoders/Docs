# Призыв дежурных из ABC
Призывает дежурных из ABC по связке "service / slug"

Пример использования:
```
  - name: Summon_abc
    abc_duty:
      service: "net"
      slug: "noc-incident-management"
    register: duty

  - startrek_comment:
      issue: "{{ startrek_issue }}"
      summonees: "{{ duty }}"
      text: Тест
```
