# @ps-int/ps-lint

Требует nodejs 12+

## Как подключить в свой проект?
`.eslintrc`:
```json
{
  "extends": "./node_modules/@ps-int/ps-lint/eslintrc.js"
}
```

`package.json`:
```json
{
  "scripts": "eslint <path_to_project_root> --ext=.js,.ts,.tsx"
}
```

## Как опубликовать новую версию?

```bash
npm run package X.Y.Z
```
