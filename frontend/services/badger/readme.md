# Badges

[![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/services/badger&vcs=arc)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=services/badger)

[Demo](https://badger.yandex-team.ru/demo)

## Startrek

Необходим доступ на чтение @robot-badger к вашей очереди

### Issue status

```
https://badger.yandex-team.ru/st/${ISSUE}/status.svg
```

Example: ```https://badger.yandex-team.ru/st/BRPAGES-10000/status.svg```

![](https://badger.yandex-team.ru/st/BRPAGES-10000/status.svg)

## Github

Доступы не требуются

### Branches diff

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/${BRANCH}/${BASE}/diff.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/demo-branch-for-readme/master/diff.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/demo-branch-for-readme/master/diff.svg)

### Pull Request diff

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/pull/${PR_NUMBER}/diff.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/pull/3/diff.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/pull/3/diff.svg)

### Pull Request Assign

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/pull/${PR_NUMBER}/assign.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/pull/1/assign.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/pull/3/assign.svg)

### Pull Request Review

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/pull/${PR_NUMBER}/review.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/pull/1/review.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/pull/3/review.svg)

### Pull Request Status

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/pull/${PR_NUMBER}/status.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/pull/1/status.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/pull/3/status.svg)

### Build PR

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/pull/${PR_NUMBER}/drone.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/pull/1/drone.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/pull/1/drone.svg)

### Build status

```
https://badger.yandex-team.ru/github/${OWNER}/${REPO}/${BRANCH}/state.svg
```

Example: ```https://badger.yandex-team.ru/github/joshuan/badger/master/state.svg```

![](https://badger.yandex-team.ru/github/joshuan/badger/master/state.svg)

## Node Package Manager

### npm package version

```
https://badger.yandex-team.ru/npm/${PACKAGE}/version.svg
```

Example: ```https://badger.yandex-team.ru/npm/islands/version.svg```

![](https://badger.yandex-team.ru/npm/islands/version.svg)

### npm package owner

```
https://badger.yandex-team.ru/npm/${PACKAGE}/owner.svg
```

Example: ```https://badger.yandex-team.ru/npm/pino-pack/owner.svg```

![](https://badger.yandex-team.ru/npm/pino-pack/owner.svg)

## OKO

### GitHub repository dependencies health

```
https://badger.yandex-team.ru/oko/repo/${REPOSITORY}/health.svg
```

Example: ```https://badger.yandex-team.ru/oko/repo/toolbox/badger/health.svg```

![](https://badger.yandex-team.ru/oko/repo/toolbox/badger/health.svg)

### GitHub monorepository dependencies health

```
https://badger.yandex-team.ru/oko/repo/${REPOSITORY}/health.svg?repoFilter=${FILTER}
```

Example: ```https://badger.yandex-team.ru/oko/repo/search-interfaces/frontend/health.svg?repoFilter=packages/i18n```

![](https://badger.yandex-team.ru/oko/repo/search-interfaces/frontend/health.svg?repoFilter=packages/i18n)

### NPM package distribution health

```
https://badger.yandex-team.ru/oko/pkg/${PACKAGE}/health.svg
```

Example: ```https://badger.yandex-team.ru/oko/pkg/islands/health.svg```

![](https://badger.yandex-team.ru/oko/pkg/islands/health.svg)

### Custom badge

```
https://badger.yandex-team.ru/custom/${PATTERN}/badge.svg
```

`${PATTERN}` consists of an arbitrary number of parts separated by `/`.

One part has a following format: `[${TEXT}][${COLOR}]`, where:

* `${TEXT}` – any text you want to add to your badge.

* `${COLOR}` (optional) – any color from [config](https://github.yandex-team.ru/toolbox/badger/blob/master/configs/defaults.js#L43) or color in hex format without `#`

Example: ```https://badger.yandex-team.ru/custom/[Custom]/[Badge][green]/badge.svg```

![](https://badger.yandex-team.ru/custom/[Custom]/[Badge][green]/badge.svg)
