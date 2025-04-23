# Webpack

Конфиги лежат в `.config`

Для построения аналитики того что доезжает в бандл, нужно выставить переменную окружения `BUNDLE_ANALYZE` - например в значение `1`, затем запустить задачу сборки вебпаком

```
BUNDLE_ANALYZE=1 npm run build:react
```

Файл отчета: `./build/static/react/report.html`
