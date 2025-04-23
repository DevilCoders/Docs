#### Как запускать?

В проекте:
```
npm run beton:update -- src/entities/**/*.js

npm run beton:migrate -- src/entities/**/*.js

git add .

eslint --fix

prettier --single-quote --trailing-comma all --no-bracket-spacing --write src/entities/**/*.js
```

