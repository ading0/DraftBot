## DraftBot
Discord bot for drafting players, auction-style, in 2 teams.


#### Usage

You will need a Discord bot token; put it in `.env` as `DISCORD_BOT_TOKEN`.
Register the bot in a server and run `main.py` to have the bot come online.
The bot listens to any text channel it has access to, and can be manipulated by typing on those channels. However, the drafting process requires some privacy, and the bot will communicate with the captains by direct messages

Most of the logic is in `draft_client.py`.
- `awaken`, `reset`, `reset_state`: reset the state of the bot completely
- `state`, `view_state`: see the current draft progress
- `setting`, `view_setting`: see the current draft rules
- `change_setting <setting> <value>` can be used to change settings
- `claim_captain` is used by a Discord user to become a captain.
- `add_player` is used to add draftable players.
- `commence`, `start`, `begin` is used to start the draft. Make sure that all players are added! The number of captains is a setting (default 2), and this command is only valid when written by a captain.

Once drafting begins, the bot will issue further instructions via direct messages. This is basically how it works, although there are some edge cases:
- Drafting gives all captains an equal amount of virtual currency.
- Each round of drafting involves all captains being given the name of a random player. Both captains must enter a private bid. The captain submitting the largest bid wins, but spends the amount of currency equal to their bid.
- Drafting continues until the remaining players can be trivially assigned to teams.
- Once drafting finishes, the results are publically announced in whatever channel `commence` was sent in.

#### Limitations
No GUI for now :(
The only drafting algorithm possible is fairly arbitrary, but due to symmetry it is definitely "fair." It might, however, be unpleasant.
