here is the fucking backend for aura 
this kid @jonesy.fnbr skidded this dont use its ass 
idc abt the token if its in there and yeah and hes saying bs
Download ---> [Download]()
# READ IF CALLED SKID
btw this is ***AI***
cant say this is lit ai lol

# Aura Backend - Complete Setup Guide

This is the complete Aura backend system with all files included.

## File Structure

Your Aura backend should have this exact folder structure:
```
Aura/
├── src/
│   ├── config/
│   │   └── config.js
│   ├── models/
│   │   ├── Profile.js
│   │   ├── Transaction.js
│   │   ├── Reward.js
│   │   ├── Cosmetic.js
│   │   └── Shop.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── user.js
│   │   ├── admin.js
│   │   ├── shop.js
│   │   └── reward.js
│   ├── services/
│   │   ├── email.js
│   │   ├── payment.js
│   │   ├── rewards.js
│   │   └── shop.js
│   ├── middleware/
│   │   ├── auth.js
│   │   ├── permissions.js
│   │   └── validation.js
│   ├── discord/
│   │   ├── bot.js
│   │   └── commands/
│   │       ├── user/
│   │       │   ├── register.js
│   │       │   ├── profile.js
│   │       │   ├── locker.js
│   │       │   ├── stats.js
│   │       │   ├── balance.js
│   │       │   ├── rewards.js
│   │       │   ├── claim.js
│   │       │   └── help.js
│   │       └── admin/
│   │           ├── ban.js
│   │           ├── unban.js
│   │           ├── givevbucks.js
│   │           ├── setvbucks.js
│   │           ├── viewaccount.js
│   │           ├── refreshshop.js
│   │           └── serverstats.js
│   ├── utils/
│   │   └── logger.js
│   └── index.js
├── logs/
├── .env
├── .env.example
├── package.json
├── Install.bat
└── Start.bat
```

## Installation Steps

### Step 1: Install Node.js

Download and install Node.js from https://nodejs.org/ (version 16 or higher recommended)

### Step 2: Install MongoDB

You need MongoDB running either:
- Locally: Download from https://www.mongodb.com/try/download/community
- Cloud: Use MongoDB Atlas at https://www.mongodb.com/cloud/atlas

### Step 3: Install Dependencies

Run Install.bat - this will:
- Check if Node.js is installed
- Install all npm packages
- Create a .env file from .env.example

### Step 4: Configure Environment Variables

Open the .env file and fill in these required settings:
```env
# Discord Bot (REQUIRED)
DISCORD_TOKEN=your_bot_token_here
DISCORD_CLIENT_ID=your_client_id
DISCORD_GUILD_ID=your_server_id

# Discord Roles (REQUIRED)
ROLE_ADMIN=your_admin_role_id
ROLE_FULLLOCKER=your_fulllocker_role_id
ROLE_ELITE_DONATOR=your_elite_donator_role_id
ROLE_BOOSTER=your_booster_role_id

# Discord Channels (REQUIRED)
CHANNEL_LOGS=your_logs_channel_id
CHANNEL_FULLLOCKER_LOGS=your_fulllocker_logs_channel_id
CHANNEL_ELITE_DONATOR_LOGS=your_elite_donator_logs_channel_id
CHANNEL_BOOSTER_LOGS=your_booster_logs_channel_id

# Database (change if using MongoDB Atlas)
MONGODB_URI=mongodb://localhost:27017/Aura

# Security (CHANGE THIS!)
JWT_SECRET=change_this_to_something_random_and_secure
```

### Step 5: Register Discord Commands

You need to register the slash commands with Discord. Create a file called `deploy-commands.js` in your Aura folder:
```javascript
const { REST, Routes } = require('discord.js');
const fs = require('fs');
require('dotenv').config();

const commands = [];
const commandFolders = ['user', 'admin'];

for (const folder of commandFolders) {
    const commandFiles = fs.readdirSync(`./src/discord/commands/${folder}`).filter(file => file.endsWith('.js'));
    for (const file of commandFiles) {
        const command = require(`./src/discord/commands/${folder}/${file}`);
        commands.push(command.data.toJSON());
    }
}

const rest = new REST({ version: '10' }).setToken(process.env.DISCORD_TOKEN);

(async () => {
    try {
        console.log('Registering slash commands...');

        await rest.put(
            Routes.applicationGuildCommands(process.env.DISCORD_CLIENT_ID, process.env.DISCORD_GUILD_ID),
            { body: commands },
        );

        console.log('Successfully registered slash commands!');
    } catch (error) {
        console.error(error);
    }
})();
```

Then run: `node deploy-commands.js`

### Step 6: Start the Backend

Run Start.bat - this will start the Aura backend server

## Discord Commands

### User Commands

- `/register` - Create a Aura account
- `/profile` - View your profile
- `/locker` - View your locker items
- `/stats` - View your statistics
- `/balance` - Check vbucks balance
- `/rewards` - View available rewards
- `/claim` - Claim rewards (elite-donator, fulllocker, booster)
- `/help` - Display help

### Admin Commands

- `/ban` - Ban a user
- `/unban` - Unban a user
- `/givevbucks` - Give vbucks to a user
- `/setvbucks` - Set a user's vbucks balance
- `/viewaccount` - View user account details
- `/refreshshop` - Manually refresh the item shop
- `/serverstats` - View server statistics

## Configuration

### Change Season and Version

Edit `.env`:
```env
PROJECT_SEASON=15
PROJECT_VERSION=12.41
```

### Elite Donator Rewards

Edit `src/config/config.js` (lines 62-89) to change:
- Vbucks amount (default: 5000)
- Item IDs and names

### Booster Rewards

Edit `src/config/config.js` (lines 90-98) to change:
- Item IDs and names

### Full Locker Rewards

Edit `src/config/config.js` (lines 99-103) to change:
- Maximum season version

### Item Shop Configuration

To change shop rotation, edit `src/services/shop.js` or use `/refreshshop` command.

## Troubleshooting

### Backend won't start
- Make sure MongoDB is running
- Check that all environment variables are set correctly
- Verify port 3000 is not already in use

### Discord bot not connecting
- Verify DISCORD_TOKEN is correct
- Make sure bot has proper permissions in your server
- Check that bot is invited to your Discord server

### Commands not showing up
- Run `node deploy-commands.js` to register commands
- Make sure DISCORD_CLIENT_ID and DISCORD_GUILD_ID are correct

## Support

All code is heavily commented to explain what each part does. If you need help, check the comments in the files.

Aura Backend - Built for Old School Fortnite
