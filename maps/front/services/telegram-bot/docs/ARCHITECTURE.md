# Architecture
The whole app is based on [node-telegram-bot-api](https://github.com/yagop/node-telegram-bot-api) package which is a very thin wrapper to [Telegram Bot Api](https://core.telegram.org/bots/api).

## Idea
I am a fun of [express](https://expressjs.com/) library. Love the idea of middlewares and pipeline of handling request.

I have tried to use the same approach for bot development.

## Basic terms
The majority of logic was put in [src/lib/bot.js](src/lib/bot.js). It is a wrapper for `node-telegram-bot-api` and it makes it possible to write Telegram bot in express like way.

```javascript
const TelegramBot = require('src/bot/lib');
const bot = new TelegramBot(options);

bot
    .use(firstMiddleware)
    .use(secondMiddleware)
    .use(errorMiddleware)
    .listen();
```

So you use add as many middlewares as you want. The last middleware is special. It is an error middleware which will be exected when an error occures in the middle of pipeline.

A middlewares can handle all request or only specific commands. I usually call such middlewares as commands.

```javascript
bot
    .use(firstMiddleware)
    .use('/lang', langCommand)
    .use(errorMiddleware)
    .listen();
```

## How does it handle messages
When bot receives a message, it will create a request object which is passed to the middlewares.

```javascript
const req = {
    msg: message // message from Telegram Api
};
```

Then the first middleware will be executed with three parameters:

  * `req` — Request.
  * `bot` — Link to the bot wrapper object.
  * `next` — Function which should be executed for going to the next middleware.

**Note.** If you forget to call `bot.sendMessage` or `next`, no error will be showed. Be careful!

## A couple of words about api directory
[src/api](src/api) directory contains code which works with external services like metasearch or traffic export or using database. There is no telegram specific logic.

There are used two libraries:

  * [bla](npmjs.com/package/bla) for creating API methods.
  * [mongoosejs](mongoosejs.com) for access to mongodb.
