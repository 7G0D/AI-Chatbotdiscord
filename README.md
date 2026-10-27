# Private AI Discord Chat

Discord bot that creates private AI chat channels and replies using Google's Gemini API.

## Requirements

- Node.js 20+
- Discord bot with **Message Content Intent** enabled
- Gemini API key from Google AI Studio

## Setup

1. Create a Discord application and bot. Invite it with the `bot` and `applications.commands` scopes and grant **Manage Channels**, **View Channels**, **Send Messages**, and **Read Message History**.
2. Copy `.env.example` to `.env` and replace the placeholders with your values:

   ```env
   DISCORD_TOKEN=your-discord-bot-token
   DISCORD_CLIENT_ID=your-discord-application-id
   DISCORD_GUILD_ID=your-discord-server-id
   CHAT_COMMAND_CHANNEL_ID=channel-for-createchat
   CHAT_CATEGORY_ID=category-for-private-chats
   GEMINI_API_KEY=your-gemini-api-key
   GEMINI_MODEL=gemini-flash-lite-latest
   GEMINI_TIMEOUT_MS=120000
   ```

   In PowerShell, copy the example with `Copy-Item .env.example .env`. Do not commit `.env`; it is ignored by Git.

3. Install dependencies, register `/createchat`, and start the bot:

   ```sh
   npm install
   npm run deploy
   npm start
   ```

## Chat behavior

- Use `/createchat` in the configured command channel. Each chat is visible only to its owner and the bot; server administrators may also have access.
- New channels use the owner's server display name.
- The **Close chat** button asks for confirmation, then permanently deletes the channel.
- The bot presence shows **Watching Chats**, rotating Online, Idle, and Do Not Disturb every 10 seconds.
- Conversation history is kept in memory and cleared when the bot restarts or the channel is deleted. Requests use `store: false`.

If a reply fails, check the bot console and the error shown in the chat. Gemini availability and quotas depend on your Google AI Studio project.
