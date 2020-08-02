# Discord.js-selfbot

This readme explains the modifications made to discord.js@12 and how to setup the selfbot-version by davidfegyver.

#### I don't take any responsibility for blocked Discord accounts that used this module.
#### Using this on a user account is prohibited by the Discord TOS and can lead to the account block.

## What is Different In The Modified Version?

### User Agent Changes

In the [Constants](https://github.com/discordjs/discord.js/blob/master/src/util/Constants.js) file, you can see that it  basically just telling discord, we are using a discord library to interact with them:
```javascript
exports.UserAgent = browser
  ? null
  : `DiscordBot (${Package.homepage.split('#')[0]}, ${Package.version}) Node.js/${process.version}`;
```
This is not good, because we want discord to think we aren't using a bot library. To fix this, those lines are replaced with this:

`exports.UserAgent = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:73.0) Gecko/20100101 Firefox/73.0';`

This is a generic user agent string, it is saying that the user is using Firefox on Windows 10.

### Authorization Changes

This change is in the [RESTManager](https://github.com/discordjs/discord.js/blob/master/src/rest/RESTManager.js) file.

Another header called Authorization. This is the header that your token is sent in.

``if (token) return `${this.tokenPrefix} ${token}`;``

From that line we can see that discord.js is sending the token with a 'Bot' prefix. 

We want to send exactly your token, so we will make the following change:

``if (token) return `${token}`;``

Now, there's no 'Bot' prefix. Just the token.


### How Do I Use The Official Discord.js?

If you want to do your own self-bot, first I would say that discord has a strong defence against self-bots, so you can get account-termination (ban).

That being said, I am not saying that by using the modified library, discord will thinking you are a legitimate human user. However, the changes that have been explained in this document should be more hard to determine if you are using a library.

Anyway, go here for instructions:

https://www.npmjs.com/package/discord.js
