# NOCRFCsd

## Изменение согласующих

Для изменения набора согласующих NOCRFC необходимо:

1. Внести изменения в [approvers.yaml](https://a.yandex-team.ru/arcadia/noc/nocrfcsd/static/approvers.yaml). Подробнее о
   формате можно почитать в [Согласовщики](https://docs.yandex-team.ru/nocrfcsd/approvers).
2. Если нет уверенности в изменениях, то провалидировать конфиг через утилиту
   `nocrfcs-validate-approvers`, подробнее в
   [Валидация конфига](https://docs.yandex-team.ru/nocrfcsd/approvers#validaciya-konfiga)
3. Одобрить PR у [Группы сетевой автоматизации](https://staff.yandex-team.ru/departments/yandex_mnt_noc_dev_dep55049/)
4. Выкатить изменение через [Arcadia CI NOCRFCsd](https://a.yandex-team.ru/projects/nocdev/ci/releases/timeline?dir=noc%2Fnocrfcsd&id=nocrfcsd)
