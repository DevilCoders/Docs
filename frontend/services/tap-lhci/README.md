# LHCI Server Docker Image

⚠️ Внимание! Стенд Lighthouse в данное время недоступен, шаги по его развертыванию описаны на [wiki-странице](https://wiki.yandex-team.ru/tap/projects/tap-lhci-deploy).

- Документация: https://github.com/GoogleChrome/lighthouse-ci

## Сборка

```bash
docker build -t registry.yandex.net/tap/lhci:v${VERSION} .
docker push registry.yandex.net/tap/lhci:v${VERSION}
```

## Запуск локально

```bash
docker-compose up -d --build
```
