# RunTime Cloud Config (formerly gencfg.upper)

Генератор конфигов репорта, ноапача и не только. Документацию можно посмотреть [здесь][1].

Установка virtualenv для работы с миграциями:

1. Установка venv (в директории gencfg.upper)
  /skynet/python/bin/virtualenv --system-site-packages venv

2. Активируем venv и добавлем PYTHONPATH
  . activate.sh

3. Устанавливаем необходимые пакеты в созданный venv
  pip install -U -r requirements.txt

Ответственный за конструкцию в целом: mvel@
Умеют читать код rtcc: aokhotin@, kotjakov@ (не занимается rtcc)
Знают про выкатку релизов rtcc и testenv: saylars@, mvel@

[1]: https://wiki.yandex-team.ru/jandekspoisk/sepe/stability/upperconfig/
