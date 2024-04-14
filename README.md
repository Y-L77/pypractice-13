import discord, requests, random
from discord.ext import commands

#this is the beta non full access cybercriminal discord tool
#message YipLuu discord to buy full ver

intents = discord.Intents.all()  # Enable all intents
client = commands.Bot(command_prefix="Σ", intents=intents)

def get_ip_info(ip_address):
    res = requests.get(f'https://ipinfo.io/{ip_address}')
    data = res.json()
    return data

pwgeni = 0
pwgenCHAR = ("!", "@", "#", "$", "%", "^", "&", "*", "-", "_", "+", ":", "Σ", "1", "2", "3", "4", "5", "6", "7", "8", "9", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U")

@client.event
async def on_ready():
    print("Bot activated")
    print("--------------")

@client.command()
async def cmds(ctx):
    message = (
        "```Σcmds = Get line of commands CC handles (beta)\n"
        "ΣGeoIP (ip address) = location of an ip (beta)\n"
        "Σpwgen(int) = generate random password (beta)\n"
        "Σhelp = Get line of commands CC handles (unfinished)\n"
        "Σwebstrengh(website) = check how strong a website is (unfinished (not for public)\n"
        "Σdata = get identity (not for pub)```"
    )
    await ctx.send(message)

@client.command()
async def GeoIP(ctx, *, ip_address=None):
    if ip_address is None:
        await ctx.send("Please provide an IP address.")
        return

    try:
        ip_info = get_ip_info(ip_address)
        info_string = "IP Information: "
        for key, value in ip_info.items():
            info_string += f"{key}: {value} | "
        await ctx.send(info_string)
    except Exception as e:
        await ctx.send("An error occurred while retrieving IP information. Please check the formatting of the IP address.")


@client.command()
async def pwgen(ctx, pwgeni: int):
    if pwgeni > 50:
        await ctx.send("Please choose a number less than 50.")
        return
    elif pwgeni <= 0:
        await ctx.send("Please provide a positive number.")
        return

    generated_password = ''.join(random.choices(pwgenCHAR, k=pwgeni))
    await ctx.send(f"Generated password: {generated_password}")

    





client.run("enter bot token here")
