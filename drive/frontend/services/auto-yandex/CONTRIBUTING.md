## Getting Started
1. `make deps`
2. `make build`

Open `out/static/index.html` in your browser.

## Deploying to testing

Update `src/static` files and:
```
make patch
git push origin branch --folow-tags
make release-testing
```

### Production
**Note.** Only project maintainer can release the project to production.

For deploying to production run the command.
```
$ npx qtools deploy production
```
or update app version manually in Deploy.
