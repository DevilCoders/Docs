Необходимо добавить поля в секреты:
- ((https://yav.yandex-team.ru/secret/{{secretId}} {{secretName}})):
    - {{applicationName}}-production-production-tvm.json
    - salt.json

В файл %%salt.json%% нужно записать случайную строку в двойных кавычках. Для генерации используйте одну из команд (или аналог):
- %%openssl rand -base64 14%%
- %%gpg --gen-random --armor 1 14%%

Для генерации твм-секретов, ((https://wiki.yandex-team.ru/Market/frontend/infra/grants/ читайте документацию))

Тикет создан автоматически [пайплайном]({{jobContext.getPipeLaunchUrl()}}) 