Anible-playbook для juggler-проверок качества поиска
Регулярно запускается шедулером таски `RUN_JUGGLER_VIDEO_QUALITY_PLAYBOOK`: https://sandbox.yandex-team.ru/scheduler/6332/view

Как запустить:

1. Получить oauth token juggler из веб-интерфеса (на момент написания ссылочка в подвале)
2. `export JUGGLER_OAUTH_TOKEN="<полученный токен>"`
3. `virtualenv venv`
4. `source venv/bin/activate`
5. `pip install --upgrade pip setuptools`
6. `pip install --index-url https://pypi.yandex-team.ru/simple/ ansible-juggler2`
7. `ansible-playbook main.yml`
