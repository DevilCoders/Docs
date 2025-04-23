# pystyle.sh

Стайлер питон кода. Вызывает сначала `isort`, потом `black`. Утилиты используют [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/ads/bsyeti/pyproject.toml?rev=r7768463).

Пример:
```bash
    $: ./ads/bsyeti/tools/pystyle/pystyle.sh ads/bsyeti/samogon/raven/test/test_plugin.py

    Fixing arcadia/ads/bsyeti/samogon/raven/test/test_plugin.py
    reformatted ads/bsyeti/samogon/raven/test/test_plugin.py
    All done! ✨ 🍰 ✨
    1 file reformatted.
```
