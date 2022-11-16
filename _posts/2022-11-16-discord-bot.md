---
title: My First Project
date: 2022-11-16 12:00
categories: [Projects]
tags: [discord, bots, javascript]      # TAG names should always be lowercase
---

# Project Nessi

For my first project I wanted to create something that would aid my discord server with 'life' with a 'AI'. That could possibly hold a conversation to an extent with myself or the 30 members in my discord server. That was the plan atleast. I started by creating the bot using the dev tools provided by discord, then poured some life (code) into it using javascript (discord.js). As this was my first ever project and my first time using js, I did not want to get burned out from countless tutorials so I started slow. When I say slow I mean "lets atleast make the bot do one thing for now" so thats what i did. I started with v13 syntax and had no idea that v14 was a thing so that was my first brain fart.

## Creating environment variables for secrets

So initially my plan was to make a chatbot using scripts from rick and morty, but i started here. How to implement slash commands on your discord bot with v14 sysntax.

```javascript
const { REST } = require('@discordjs/rest');
const { Routes } = require('discord-api-types/v9');

const commands = [{
  name: 'ping',
  description: 'Replies with Pong!'
}]; 

const rest = new REST({ version: '9' }).setToken('token');

(async () => {
  try {
    console.log('Started refreshing application (/) commands.');

    await rest.put(
      Routes.applicationGuildCommands(CLIENT_ID, GUILD_ID),
      { body: commands },
    );

    console.log('Successfully reloaded application (/) commands.');
  } catch (error) {
    console.error(error);
  }
})();
```
The first step being to store our ID's and tokens as enviorment variables. The code above shows the raw format that will be changed with your own personal ID's and Bot token. This is done inside the index.js file.

The next step was to specify your own commands: 

```javascript
const commands = [{
  name: 'nessi',
  description: 'Replies with ABULAGRODADEM!'
}];
```
After this step you make 'token' a variable.

```javascript
const rest = new REST({ version: '9' }).setToken(token);
```
Next step was to create the initial bot program in a new file called bot.js.

```javascript
const { Client, Intents } = require('discord.js');
const client = new Client({ intents: [Intents.FLAGS.GUILDS] });

client.on('ready', () => {
  console.log(Logged in as ${client.user.tag}!);
});

client.on('interactionCreate', async interaction => {
  if (!interaction.isCommand()) return;

  if (interaction.commandName === 'ping') {
    await interaction.reply('Pong!');
  }
});

client.login('token');
```
This is the code for our new bot.js file that we have created for the program. During this stage you have to copy your token variable from index.js and post it to the bot.js file then make sure the token is the variable.

Then define your slash commands. 

When creating a bot you will have a package.json file. You will have to update the file to run the bot with bot.js instead of index.js. Then run the program with VScode or anything else that you use.

## Woo a working slash command!

![img-description](https://cdn.discordapp.com/attachments/1042526278118543450/1042534452783489094/image.png)

I first tested the bot myself, then invited a friend to see if he would get the same result.