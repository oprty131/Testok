import discord
import openai
import os

# Retrieve your OpenAI API key and Discord bot token from environment variables
OPENAI_API_KEY = os.getenv('OPENAI_API_KEY')
DISCORD_TOKEN = os.getenv('DISCORD_TOKEN')

openai.api_key = OPENAI_API_KEY

intents = discord.Intents.default()
intents.messages = True

client = discord.Client(intents=intents)

@client.event
async def on_ready():
    print(f'We have logged in as {client.user}')

@client.event
async def on_message(message):
    # Don't let the bot reply to itself
    if message.author == client.user:
        return

    # Check if the message starts with a specific command (e.g., "!ask")
    if message.content.startswith('!ask'):
        prompt = message.content[len('!ask '):]  # Get the prompt after the command

        try:
            response = openai.ChatCompletion.create(
                model='gpt-3.5-turbo',
                messages=[{'role': 'user', 'content': prompt}]
            )
            answer = response['choices'][0]['message']['content']
            await message.channel.send(answer)
        except Exception as e:
            await message.channel.send(f'Error: {str(e)}')

# Run the bot
client.run(DISCORD_TOKEN)
