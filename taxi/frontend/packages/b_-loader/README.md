# Webpack b_ loader

# Установка

    npm i --save-dev @yandex-taxi/b_-loader
    
Loader должен идти самым последним

```javascript
const css = [
    {loader: '@yandex-taxi/b_-loader'},
    {loader: 'style-loader', options: {sourceMap: false}},
    {loader: 'css-loader', options: {sourceMap: false}},
    {loader: 'postcss-loader', options: {sourceMap: false}}
];
```

# Разработка

Линтинг
    
    npm run lint
    npm run test
    npm run fix

Релиз

    npm run prepare-release
    git push --follow-tags origin master && npm publish
    
