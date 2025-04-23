# Billing Continuous Integration Scripts

## Hosts
```
greed-dev3f.balance.os.yandex.ru
greed-dev3g.balance.os.yandex.ru
```

## How to restart agents
```bash
/etc/init.d/teamcity-agent restart {AGENTNAME}
```

## Available agents
[Billing pool](https://teamcity.yandex-team.ru/agents.html?tab=agentPools#58)<br />
[Billing Testing pool](https://teamcity.yandex-team.ru/agents.html?tab=agentPools#90)

`static` means `fixed license` (don't use [License Server](https://wiki.yandex-team.ru/teamcity/pluginlicenseserver/))

## Wiki
Search by `TeamCity` keyword<br />
[Разработка интерфейсов Баланса](https://wiki.yandex-team.ru/billing/balance/dev/ui/)

## billing.buildBranch
To update `billing.buildBranch` add build configuration to `teamcity_deploy/services/config.py:54`
