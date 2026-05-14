> Next generation of the Dashboard is out! <br>
> https://github.com/SonMooSans/discord-bot-dashboard-2

![Demo](document/img.png)

# D-Dash: Discord Bot Dashboard

A Full-Featured Dashboard Template for Discord Bots
<br>
You can modify `config/config.js` to edit configuration without touching the codes
<br>
Feel free to contribute this project

**Watch the Demo on [YouTube](https://youtu.be/Z90Ax-v4uH4)**

## Features
* Modern Design with Chakra UI
* Localization Support (English and Chinese)
* Customizable UI (`config.js`)
* Built-in **Features** and **Actions** System
* Existing Backend Implementation

## Getting Started
**First, clone this Template**
```
git clone https://github.com/SonMooSans/discord-bot-dashboard.git
```

D-Dash is not just a Template, it supports to add **Feature** and **Action** in configuration
<br>
Therefore, it requires a full Backend Implementation.
<br>
For the implementation in Kotlin, See the [Example](https://github.com/SonMooSans/discord-bot-dashboard-backend)

You may implement your own Backend APi in another languages by implementing routes mentioned in its README

## Configuration
Go to the [config.js](src/config/config.js)
<br>
This configuration allows you to customize the UI, there is a `config.d.ts` for type annotations

### Normal Settings
You need to specify the API Url and invite url of your bot
<br>
You might also add footer items in configuration
```javascript
const config = {
    name: "Bot Name",
    footer: [
        {
            name: "Hello World",
            url: "https://github.com"
        }
    ],
    //API url
    serverUrl: "http://localhost:8080",
    //Invite url of your bot
    inviteUrl: "https://discord.com/api/oauth2/authorize?client_id=1004280473956139038&permissions=8&scope=bot",
}
```

### Display Data or Statistics
You can customize data to display in your dashboard.
<br>
#### Items function
it reads `detail` and `state`, then returns `DataItem` array which determines what to display

#### Dashboard Data
It is an Array of Dashboard Data Row, you can customize options of each row to get additional data from `state`

Each Data Row contains a items function
<br>
You can set `advanced` to true, so the dashboard will fetch `/guild/:guild/detail/advanced` and pass the result to the function by `state.advanced`
It will be displayed in **Statistics** Tab

#### Actions and Features Data
They are both **Items function**

It will be displayed in **Actions** and **Features** Tab
<br>
you can display the statistics of things like **Ranks**, **Reaction Role** 

```javascript
const config = {
    data: {
        dashboard: [
            {
                advanced: true,
                count: 3, //count of placeholders
                //advanced will be null if row.advanced is false
                items: (detail, {advanced}) => [
                    DataItem
                ]
            }
        ],
        actions: detail => [
            DataItem
        ],
        features: detail => [
            DataItem
        ]
    }
}
```

### Features and Actions
You must define bot features and actions in configuration
<br>
Also, the Features and Actions System must be implemented at your API

#### Feature
**Feature** is something that can be enabled or disabled, after enabling a feature.
<br>
User can edit its options and customize the behavior of bot

#### Action
**Action** contains multi **Tasks**, User can publish or delete Tasks
<br>
User must define some options before publishing a task

Action can be used for `Reaction Role` since you might want the Reaction Role can be enabled for multi messages

#### Options
Each Feature and Action requires an options array used to customize settings
<br>
When user updates options, server will receive a map of ids and its value

The **Options Function** will receive the `values` of feature/action fetched from server
<br>
For **Action**, values will be null before user publish the Task

```javascript
const config = {
    features: {
        "id_of_feature": {
            name: "Welcome Message",
            description: "Send a Mesage to welcome a member when they just joined the Server",
            options: (values) => [
                //Example option
                {
                    id: "message",
                    name: "Message",
                    description: "The message to be sent",
                    type: OptionTypes.Message_Create, //A Message/Embed Creator 
                    value: values? values.message : "",
                }
            ]
        }
    },
    actions: {
        "id_of_action": {
            name: "Reaction Role",
            description: "Give user a role when reacts to a Message",
            //values will be null before user publish the Task
            options: (values) => [
                //Example option
                {
                    id: "message",
                    name: "Message",
                    description: "The message to be sent",
                    type: OptionTypes.Message_Create, //A Message/Embed Creator 
                    value: values? values.message : "",
                },
            ]
        }
    }
}
```

### Multi Languages
Some fields support Multi Languages
<br>
You can see their type annotations to check about it

For those fields, you can use: 
```javascript
text = {
    zh: "Chinese",
    en: "English"
}
```

For now, we only supports **English (en)** or **Chinese (zh)**.
<br>
You can use `<Locale zh="Chinese" en="English" />` on some fields since they may supports `JSXElement`

## the Template of Template
This Dashboard is Based on [Horizon UI ⚡️](https://horizon-ui.com/horizon-ui-chakra)

---

# EmoStatic 2.1 - All-in-One Discord Bot

## Overview
EmoStatic 2.1 is a comprehensive all-in-one Discord bot featuring Administrative & Security tools, Community Engagement systems, and Entertainment features. All commands are implemented as **Slash Commands** (`/command`) for enhanced user experience and accessibility.

## Command Categories & Slash Commands

### 🛡️ Administrative & Security

#### Moderation Commands
- `/mute <user> [duration] [reason]` - Mute a user for a specified duration
- `/unmute <user>` - Remove mute from a user
- `/kick <user> [reason]` - Kick a user from the server
- `/ban <user> [reason] [duration]` - Ban a user (temporary or permanent)
- `/unban <user>` - Unban a previously banned user
- `/warn <user> <reason>` - Issue a warning to a user
- `/clearwarns <user>` - Clear all warnings for a user
- `/warnings <user>` - View warnings for a specific user

#### Automod & Filters
- `/automod enable` - Enable automated moderation
- `/automod disable` - Disable automated moderation
- `/filter add <word>` - Add a word to the banned words filter
- `/filter remove <word>` - Remove a word from the filter
- `/filter list` - View all filtered words
- `/spam-settings <sensitivity>` - Configure spam detection sensitivity (1-10)
- `/link-filter enable|disable` - Toggle malicious link filtering

#### Verification & Security
- `/verification setup` - Set up server verification system
- `/verification enable <type>` - Enable verification (captcha/rules)
- `/verification disable` - Disable verification system
- `/captcha-settings <difficulty>` - Configure captcha difficulty
- `/rules-screen configure` - Set up rules screening for new members

#### Logging & Audit
- `/logs channel <channel>` - Set the logging channel
- `/logs enable <type>` - Enable logging for specific events (messages, roles, joins, etc.)
- `/logs disable <type>` - Disable logging for specific events
- `/logs view [limit]` - View recent logs (default: 25 entries)
- `/audit <user> [action]` - View audit trail for a user's actions
- `/message-history <user> [limit]` - View message history of a user

### 🎯 Management & Automation

#### Welcome & Onboarding
- `/welcome setup` - Configure welcome message system
- `/welcome message <message>` - Set custom welcome message
- `/welcome channel <channel>` - Set welcome message channel
- `/welcome embed [title] [description] [color]` - Create custom welcome embed
- `/welcome role <role>` - Auto-assign role to new members
- `/welcome enable` - Enable welcome system
- `/welcome disable` - Disable welcome system

#### Reaction Roles
- `/reactionrole create <message-id>` - Create reaction role menu
- `/reactionrole add <message-id> <emoji> <role>` - Add emoji-role pair
- `/reactionrole remove <message-id> <emoji>` - Remove emoji-role pair
- `/reactionrole list <message-id>` - View all reaction roles on a message
- `/reactionrole delete <message-id>` - Delete reaction role menu

#### Custom Commands
- `/customcmd create <name> <response>` - Create a custom command
- `/customcmd edit <name> <new-response>` - Edit a custom command
- `/customcmd delete <name>` - Delete a custom command
- `/customcmd list` - View all custom commands
- `/customcmd info <name>` - View custom command details

#### Server Utilities
- `/serverinfo` - Display detailed server statistics and information
- `/botinfo` - View bot status, uptime, and statistics
- `/members` - Display total member count and analytics
- `/roles` - View server role hierarchy
- `/channels` - List all server channels with details
- `/uptime` - Check bot uptime
- `/ping` - Display bot latency

### 👥 Community Engagement

#### Levelling & XP System
- `/level` - Check your current level and XP
- `/leaderboard [page]` - View server level leaderboard
- `/xp-settings multiplier <value>` - Set XP multiplier (for admins)
- `/xp-settings enable|disable` - Toggle XP system
- `/profile [user]` - View user profile with level and stats
- `/rank-reward <level> <role>` - Set role reward for achieving a level

#### Social Alerts & Integrations
- `/social-alert twitch <channel> <username>` - Get notifications when Twitch user goes live
- `/social-alert youtube <channel> <channel-url>` - Get notifications for new YouTube uploads
- `/social-alert reddit <channel> <subreddit>` - Get notifications for new Reddit posts
- `/social-alert x <channel> <username>` - Get notifications for new tweets
- `/social-alert remove <type>` - Remove a social alert
- `/social-alert list` - View all active social alerts

#### Giveaways & Polls
- `/giveaway create <prize> <duration> [winner-count]` - Start a giveaway
- `/giveaway end <message-id>` - End a giveaway early
- `/giveaway reroll <message-id> [winner-count]` - Reroll giveaway winners
- `/giveaway list` - View active giveaways
- `/poll create <question> [option1] [option2] [option3] [option4]` - Create a poll
- `/poll end <message-id>` - Close a poll and show results
- `/poll results <message-id>` - Display current poll results

#### Economy System
- `/balance [user]` - Check your or another user's balance
- `/daily` - Collect daily currency reward
- `/weekly` - Collect weekly currency reward
- `/transfer <user> <amount>` - Transfer currency to another user
- `/shop` - View available items in the shop
- `/buy <item> [quantity]` - Purchase item from shop
- `/inventory` - View your purchased items
- `/leaderboard-money [page]` - View richest users leaderboard
- `/gambling-settings enable|disable` - Toggle gambling features (admin)
- `/slots [amount]` - Play slot machine game with currency stakes
- `/blackjack [amount]` - Play blackjack with currency

### 🎮 Entertainment & Media

#### Music System
- `/play <song-name-or-url>` - Play a song or search and play
- `/skip` - Skip current song
- `/stop` - Stop playback and clear queue
- `/pause` - Pause current playback
- `/resume` - Resume playback
- `/queue` - View current queue
- `/queue-add <position> <song>` - Add song to queue at position
- `/queue-remove <position>` - Remove song from queue
- `/queue-clear` - Clear entire queue
- `/playlist create <name>` - Create new playlist
- `/playlist add <name> <song>` - Add song to playlist
- `/playlist remove <name> <song>` - Remove song from playlist
- `/playlist load <name>` - Load and play a playlist
- `/playlist list` - View all playlists
- `/nowplaying` - Display currently playing song
- `/volume <percentage>` - Set playback volume (0-100)
- `/loop <off|track|queue>` - Set loop mode
- `/shuffle on|off` - Toggle shuffle mode
- `/lyrics [song-name]` - Get lyrics for current or specified song

#### Mini Games
- `/trivia [difficulty]` - Start trivia game (easy/medium/hard)
- `/guess-number [range]` - Guess the number game
- `/counting-game` - Start a server-wide counting game
- `/cards play` - Play card games
- `/hangman [word-category]` - Play hangman
- `/20questions` - Play 20 questions game
- `/riddle` - Get a random riddle to solve
- `/scramble` - Unscramble the word
- `/wordle` - Play Wordle-style game

#### Fun & Anime
- `/meme` - Get a random meme
- `/anime-waifu` - Get a random anime waifu
- `/anime-husbando` - Get a random anime husbando
- `/anime-quote` - Get a random anime quote
- `/dog` - Get a random dog image
- `/cat` - Get a random cat image
- `/8ball <question>` - Ask the magic 8 ball
- `/rate <thing>` - Rate something (1-10)
- `/roast [user]` - Get a funny roast
- `/compliment [user]` - Get a compliment

#### Voice Tracking & Analytics
- `/voice-stats [user]` - View voice activity statistics
- `/voice-leaderboard [type]` - View voice activity leaderboard
- `/voice-settings enable|disable` - Toggle voice tracking
- `/temp-channels enable` - Enable temporary voice channels
- `/temp-channels create-template [name] [limit]` - Create temporary channel template
- `/temp-channels list` - View temporary channel templates
- `/activity-report` - Generate server activity report

## Permission Requirements

Each command requires specific permissions:
- **Admin Only**: `/mute`, `/unmute`, `/kick`, `/ban`, `/unban`, `/warn`, `/clearwarns`, `/automod`, `/filter`, `/verification`, `/logs`, `/welcome`, `/reactionrole`, `/customcmd`, `/xp-settings`, `/gambling-settings`, `/spam-settings`, `/link-filter`
- **Moderator+**: `/warnings`, `/audit`, `/message-history`
- **Everyone**: Most entertainment and personal stat commands

## Installation & Setup

1. Ensure the bot has necessary permissions (Administrator recommended)
2. Configure bot settings via dashboard or setup commands
3. Enable desired features and systems
4. Customize commands and responses in configuration

## Support
For issues or feature requests, please refer to the GitHub repository documentation.
