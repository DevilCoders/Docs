## Run example
```
$ nvm use
$ npm i
$ npm start
```

Run with printing API responses:
```
$ DEBGU=1 npm start
```

## Generate feed for Altay
Create table with schema (only once)
```
$ npm run create-yt-table
```
then generate feed
```
$ npm run create-altay-feed
```
