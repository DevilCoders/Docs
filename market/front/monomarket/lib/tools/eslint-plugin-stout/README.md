[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/tools/eslint-plugin-stout)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/tools/eslint-plugin-stout) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=eslint-plugin-stout)](https://oko.yandex-team.ru/pkg/eslint-plugin-stout)

# eslint-plugin-stout

Rule to disallow stout service locator

![image](https://github.yandex-team.ru/storage/user/4775/files/da94e5a8-cefe-11e7-8711-2e60d2e9094f)

    
## Install

```sh
npm i git://github.yandex-team.ru/ashelshsky/eslint-plugin-stout.git
```

## Usage
In your `.eslintrc`:

```javascript
{
  "plugins": [
    "stout"
  ],
  "rules": {
    "stout/no-service-locator": "error"
  }
}
```
