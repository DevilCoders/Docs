# Set of configs for most popular linters

## Usage

> npm i -D @yandex-int/lint --registry=http://npm.yandex-team.ru

### ESLint

__.eslintrc__:
``` json
{
  "extends": "./node_modules/@yandex-int/lint/eslintrc.js"
}
```

### Stylelint

__.stylelintrc__:
``` json
{
  "extends": "./node_modules/@yandex-int/lint/stylelintrc.js"
}
```

### Lint-Staged

__.lintstagedrc.js__:
``` javascript
const CI = process.env.TRENDBOX_CI;

module.exports = {
    linters: {
        '*.{js,jsx,ts,tsx}': [`eslint --no-ignore ${ CI ? '--quiet --output-file report-eslint.txt' : '' }`],
        '*.{css,scss}': [`${ CI ? 'sh -c "stylelint $* > $0" report-stylelint.txt' : 'stylelint'}`]
    }
};
```

### Husky

__.huskyrc__:
``` json
{
  "hooks": {
    "pre-commit": "npm run precommit"
  }
}
```

### Scripts

__package.json__:
``` json
  // ...
  "scripts": {
    "precommit": "lint-staged",
    "lint": "run-p --continue-on-error eslint stylelint",
    "eslint": "eslint --ext .js,.jsx,.ts,.tsx .",
    "stylelint": "stylelint 'src/**/*.{css,scss}'"
  },
  // ...
```
