# linebot

  [![NPM Version][npm-image]][npm-url]
  [![NPM Dependencies][dependencies-image]][dependencies-url]
  [![NPM Downloads][downloads-image]][downloads-url]

LINE Messaging API for Node.js

# About LINE Messaging API

Please refer to the official API documents for details.

https://devdocs.line.me

# Installation

```bash
$ npm install linebot --save
```

# Usage

```js
var linebot = require('linebot');

var bot = linebot({
	channelId: [CHANNEL_ID],
	channelSecret: [CHANNEL_SECRET],
	channelAccessToken: [CHANNEL_ACCESS_TOKEN]
});

bot.on('message', function (event) {
	event.reply(event.message.text).then(function (data) {
		// success
	}).catch(function(error) {
		// error
	});
});

bot.listen('/linewebhook', 3000);
```

# API

## linebot(options)
Create LineBot object.
```js
{
	verify: true // Verify `X-Line-Signature` header
}
```

## LineBot.listen(webHookPath, port, callback)

Start [Express.js](http://expressjs.com/) web server on the specified `port`,
and accept POST request callback on the specified `webHookPath`.

## LineBot.on(eventType, eventObject)

Raised when an [event](https://devdocs.line.me/en/#webhook-event-object) is received.
```js
bot.on('message',  function (event) { });
bot.on('follow',   function (event) { });
bot.on('unfollow', function (event) { });
bot.on('join',     function (event) { });
bot.on('leave',    function (event) { });
bot.on('postback', function (event) { });
```
## Event.reply(message)

Reply with message.
`message` can be a string, a [Message](https://devdocs.line.me/en/#send-message-object) object, or an array of Message objects

Return a [Promise](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise) object from [`node-fetch`](https://github.com/bitinn/node-fetch) module.

```js
event.reply('Hello, world');

event.reply({ type: 'text', text: 'Hello, world' });

event.reply({
	type: 'image',
	originalContentUrl: 'https://example.com/original.jpg',
	'previewImageUrl": "https://example.com/preview.jpg'
});
```

# License

  [MIT](LICENSE)
  
[npm-image]: https://img.shields.io/npm/v/linebot.svg
[npm-url]: https://npmjs.org/package/linebot
[dependencies-image]: https://david-dm.org/boybundit/linebot.svg
[dependencies-url]: https://david-dm.org/boybundit/linebot
[downloads-image]: https://img.shields.io/npm/dm/linebot.svg
[downloads-url]: https://npmjs.org/package/linebot
