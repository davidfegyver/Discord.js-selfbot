# Discord.js-selfbot

Ez a dokumentum leírja a módosításaimat amit a discord.js@12-n csináltam hogy selfbotoláshoz alkalmas legyen. 

#### Nem vállalok felelősséget a kibannolt fiókokért amit ezzel a könyvtárral használtál.
#### Egy felhasználói fiókkal való használat a Discord TOS (Felhasználási feltételek) ellen szól. Csak tanulási célra!! 

## Mi más a sajátz verziómban?

### User Agent Változtatások

A [Constants](https://github.com/discordjs/discord.js/blob/master/src/util/Constants.js) fájlban, láthatod hogy ez elmondja a Discordnak hogy mi egy Könyvtárat használunk a kapcsodáshoz:
```javascript
exports.UserAgent = browser
  ? null
  : `DiscordBot (${Package.homepage.split('#')[0]}, ${Package.version}) Node.js/${process.version}`;
```
Ez nem jó mivel így nem tudunk felhasználói tokennel kapcsolódni. Hogy ezt kijavítsuk, cseréljük le az előbbi sort erre:

`exports.UserAgent = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:73.0) Gecko/20100101 Firefox/73.0';`

Ez egy általános User Agent, Elmondja hogy mi egy Windows 10 gépről, egy Firefox böngészőböl kapcsolódunk.

### Autentikációs Váloztatások

Ez a [RESTManager](https://github.com/discordjs/discord.js/blob/master/src/rest/RESTManager.js) fájlban található.

Egy másik header, az Autentikációs elküldi a tokenünket.

``if (token) return `${this.tokenPrefix} ${token}`;``

Viszont itt láthatjuk, hogy egy Bot prefixxel küldi el, és nem a tiszta tokent.

Mi csak a tokent akarjuk, szóval cseréljük le az előbbi sort erre:

``if (token) return `${token}`;``

Mostmár nincs Bot prefix.


### Hogyan használjuk?
Ha ezt használni akarod, elmondom hogy a Discordnak nagyon erős védelme van a self-botokkal szemben, szóval akár kaphatsz bant is.

Attól hogy egy változtatott könyvtárat használsz, a Discord nem mindenképpen hiszi azt hogy egy teljesen legit emberi felhasználó vagy. De így nehezebb lesz eldönteniük hogy bot vagy ember vagy e.

Egyébként itt van a link:

https://www.npmjs.com/package/discord.js