# New project template

This repository is managed by [Lerna.js](https://github.com/lerna/lerna#readme).

## Getting started
```bash
npm run deps
npm run dev
```

## Directories
- `project` main project directory
- `mocks` mocks of internal packages

## Managing project-specific dependencies
### Add dependency
```bash
npx lerna add <package>
```
### Add development dependency
```bash
npx lerna add --dev <package>
```
### Uninstall dependency
First - manually delete `<package>` from `project/package.json`, then do the following:
```bash
cd ./project
rm -rf node_modules
cd ../
npx lerna bootstrap
```

### Uploading data to bunker
`BUNKER_TOKEN=your_oauth_token node ./scripts/upload-bunker.js`
