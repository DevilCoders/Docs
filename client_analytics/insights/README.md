## Misc

Загрузить шаблоны на yt:
```bash
find *.jinja2 -maxdepth 0 | xargs -I{} sh -c "cat {} | yt upload //home/vipplanners/insights/data/template/{}"
```