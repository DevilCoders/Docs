# Contribution Guide

This document describes some points about contribution process for feedback-admin.

See [Yandex Maps codestyle](https://github.yandex-team.ru/maps/maps/blob/master/codestyle.md).

## Local setup

```
npm i
npm run local
npm run dev
```

Then open `https://feedback-admin.dev.c.maps.yandex-team.ru:8080/` (maybe you want add `.ssl/ssl.crt` to your keychain).

## Release

```
npx qtools tag patch
npm version $VERSION # from previous step
# Merge PR
npx qtools release testing -f
```
