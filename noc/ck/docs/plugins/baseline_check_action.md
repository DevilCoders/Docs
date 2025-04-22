# baseline_check - сравнить бейзлайны устройства

Сравнивает текущее состояние устройства с состоянием собранным ранее через baseline_collect.

Примeр: ждем что все ipv6 bgp сесcии после изменений на устройстве поднялись, в течении 10 минут.

```yaml
      - name: collect info
        baseline_collect:
          - bgp.peers.ipv6

      # ... какие-то изменения в bgp

      - name: check baselines
        baseline_check:
          wait: "10m"
          checks:
              - op: eq
                pattern: bgp.peers.ipv6
```

Набор доступных безлайнов определен в отдельном модуле [comocutor-contrib](https://a.yandex-team.ru/arc_vcs/noc/comocutor-contrib/comocutor_contrib/data/baseline.yml)
