## Образ для тестивроания deb-пакетов Доставки в Qloud

В образ предустановлен yamail-postfix с конфигами окружений.

[Сборка в sandbox](https://sandbox.yandex-team.ru/task/555300338/view)

Важные поля сборочной джобе:
- Apply patch
- Custom version

Краткое описание работы образа:
- При вызове entyrpoint устанавливается список пакетов из переменной окружения ```PACKAGES```.
- Через перменную окружения```CONFIG_NAME``` можно (пере)определить тип кластера (yaback, mxback итд)

QA-окружения в Qloud:
- https://platform.yandex-team.ru/projects/mail/nwsmtp/qa
- https://platform.yandex-team.ru/projects/mail/nwsmtp-corp/qa

Секреты лежат тут: https://yav.yandex-team.ru/secret/sec-01dq4zy4r5bbeh1q93z5d9pym9/
Загружаеются при вызове entrypoint.
