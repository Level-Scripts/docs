# Installation

1. Put `lvl_scoreboard` into your resources.
2. Add it to `server.cfg` after lvl\_core:

```
ensure lvl_core
ensure lvl_scoreboard
```

3. Optional, for Discord avatars, names and role icons:
   1. Create a bot in the [Discord Developer Portal](https://discord.com/developers/applications) and turn on **Server Members Intent**.
   2. Invite the bot to your Discord server.
   3. Add the token to `server.cfg`:

```
set lvl_scoreboard_token "YOUR_BOT_TOKEN"
```

   4. Put your Discord server (guild) ID into `config_server.lua`.

{% hint style="danger" %}
Never put the bot token into `config.lua`. Players download that file. Use the convar or `config_server.lua`.
{% endhint %}
