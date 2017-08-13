import discord
import asyncio
from discord.ext.commands import Bot
from discord.ext import commands
import save_file
import random
import sys

Client = discord.Client()
bot_prefix = "&"
client = commands.Bot(command_prefix=bot_prefix)


@client.event
async def on_ready():
    print("Bot Online!")
    await client.change_presence(game=discord.Game(name="Standing by"))


@client.command(pass_context=True)  
async def ping(ctx):
    await client.say("Pong!")


bank_dic = save_file.a2
new_acc = save_file.a3
pistol_dic = save_file.a4
smg_dic = save_file.a5
rifle_dic = save_file.a6
tank_dic = save_file.a7
plane_dic = save_file.a8
armed_weapons = {}



class pistol:
    instances = dict()

    def __init__(self,nam, damage, cost):
        self.nam = nam
        self.damage = damage
        self.cost = cost

pist = pistol("pistol", 28, 320)

class smg:
    instances = dict()

    def __init__(self,nam, damage, cost):
        self.nam = nam
        self.damage = damage
        self.cost = cost

smgg = smg("smg", 56, 600)

class rifle:
    instances = dict()

    def __init__(self,nam, damage, cost):
        self.nam = nam
        self.damage = damage
        self.cost = cost

riflee = rifle("rifle", 89, 1120)


class tank:
    instances = dict()

    def __init__(self,nam, damage, cost):
        self.nam = nam
        self.damage = damage
        self.cost = cost

tankk = tank("tank", 380, 9910)


class plane:
    instances = dict()

    def __init__(self,nam, damage, cost):
        self.nam = nam
        self.damage = damage
        self.cost = cost

planee = plane("plane", 450, 17700)


@client.command(pass_context=True)
async def buy_pistol(ctx):
    if int(bank_dic[int(ctx.message.author.id)]) >= pist.cost:
        await client.send_message(ctx.message.channel, "[Buying pistol]: Give your pistol a name (Type &name <name>)")

        def check(msg):
            return msg.content.startswith("&name ")

        message = await client.wait_for_message(author=ctx.message.author, check=check)
        name = message.content[len("&name "):].strip()
        bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] - pist.cost

        a = pistol('{}'.format(name), random.randrange(40,60), 320)
        pistol_dic[int(ctx.message.author.id)] = getattr(a, "nam")
        await client.send_message(ctx.message.channel, "Bought {}".format(name)+" For $"+str(pist.cost))


@client.command(pass_context=True)
async def buy_smg(ctx):
    if int(bank_dic[int(ctx.message.author.id)]) >= smgg.cost:
        await client.send_message(ctx.message.channel, "[Buying SMG]: Give your SMG a name (Type &name <name>)")

        def check(msg):
            return msg.content.startswith("&name ")

        message = await client.wait_for_message(author=ctx.message.author, check=check)
        name = message.content[len("&name "):].strip()
        bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] - smgg.cost

        a = smg('{}'.format(name), random.randrange(40,60), 320)
        smg_dic[int(ctx.message.author.id)] = getattr(a, "nam")
        await client.send_message(ctx.message.channel, "Bought {}".format(name)+" For $"+str(smgg.cost))


@client.command(pass_context=True)
async def buy_rifle(ctx):
    if int(bank_dic[int(ctx.message.author.id)]) >= riflee.cost:
        await client.send_message(ctx.message.channel, "[Buying Rifle]: Give your Rifle a name (Type &name <name>)")

        def check(msg):
            return msg.content.startswith("&name ")

        message = await client.wait_for_message(author=ctx.message.author, check=check)
        name = message.content[len("&name "):].strip()
        bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] - riflee.cost

        a = pistol('{}'.format(name), random.randrange(40,60), 320)
        rifle_dic[int(ctx.message.author.id)] = getattr(a, "nam")
        await client.send_message(ctx.message.channel, "Bought {}".format(name)+" For $"+str(riflee.cost))


@client.command(pass_context=True)
async def buy_tank(ctx):
    if int(bank_dic[int(ctx.message.author.id)]) >= tankk.cost:
        await client.send_message(ctx.message.channel, "[Buying Tank]: Give your tank a name (Type &name <name>)")

        def check(msg):
            return msg.content.startswith("&name ")

        message = await client.wait_for_message(author=ctx.message.author, check=check)
        name = message.content[len("&name "):].strip()
        bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] - tankk.cost

        a = tank('{}'.format(name), random.randrange(40,60), 320)
        smg_dic[int(ctx.message.author.id)] = getattr(a, "nam")
        await client.send_message(ctx.message.channel, "Bought {}".format(name)+" For $"+str(tankk.cost))


@client.command(pass_context=True)
async def buy_fighterjet(ctx):
    if int(bank_dic[int(ctx.message.author.id)]) >= planee.cost:
        await client.send_message(ctx.message.channel, "[Buying Fighter Jet]: Give your jet a name (Type &name <name>)")

        def check(msg):
            return msg.content.startswith("&name ")

        message = await client.wait_for_message(author=ctx.message.author, check=check)
        name = message.content[len("&name "):].strip()
        bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] - planee.cost

        a = plane('{}'.format(name), random.randrange(40,60), 320)
        plane_dic[int(ctx.message.author.id)] = getattr(a, "nam")
        await client.send_message(ctx.message.channel, "Bought {}".format(name)+" For $"+str(planee.cost))

@client.command(pass_context=True)
async def armoury(ctx):
    await client.say(str(pistol_dic[int(ctx.message.author.id)]))


@client.command(pass_context=True)
async def arm(ctx):
    await client.send_message(ctx.message.channel, "Here is a list of firearms you own \n" +
                              "\n"+"[Pistol]:" +str(pistol_dic[int(ctx.message.author.id)])+
                              "\n"+"[SMG]:" +str(smg_dic[int(ctx.message.author.id)])+
                              "\n"+"[Rifle]:" +str(rifle_dic[int(ctx.message.author.id)])+
                              "\n choose one")

    def check(msg):
        return msg.content.startswith("&choose ")

    message = await client.wait_for_message(author=ctx.message.author, check=check)
    name = message.content[len("&choose "):].strip()
    if '{}'.format(name) in pistol_dic[int(ctx.message.author.id)] or smg_dic[int(ctx.message.author.id)] or rifle_dic[int(ctx.message.author.id)]:
        armed_weapons.update({str(ctx.message.author): str(name)})
        await client.send_message(ctx.message.channel, str(ctx.message.author)+" has been armed with "+str(armed_weapons[str(ctx.message.author)]))


@client.command(pass_context=True)
async def enter(ctx):
    await client.send_message(ctx.message.channel, "Here is a list of vehicles you own \n" +
                              "[Vehicle]:" +str(tank_dic[int(ctx.message.author.id)])+
                              "\n"+"[Aircraft]:" +str(plane_dic[int(ctx.message.author.id)])+
                              "\n choose one")

    def check(msg):
        return msg.content.startswith("&choose ")

    message = await client.wait_for_message(author=ctx.message.author, check=check)
    name = message.content[len("&choose "):].strip()
    if str('{}'.format(name)) == str(tank_dic[int(ctx.message.author.id)]) or str(plane_dic[int(ctx.message.author.id)]):
        armed_weapons.update({str(ctx.message.author): str(name)})
        await client.send_message(ctx.message.channel, str(ctx.message.author)+" has entered "+str(armed_weapons[str(ctx.message.author)]))


@client.event
async def on_message(message):
    await client.process_commands(message)
    if message.content.startswith("&addbank"):
        role = "Bank Manager"
        for r in message.author.roles:
            if r.name == role:
                await client.send_message(message.channel, "[Adding to Central Bank]: How much? (Type in &add <amount>)")

                def check(msg):
                    return msg.content.startswith("&add ")
                message = await client.wait_for_message(author=message.author, check=check)
                name = message.content[len("&add "):].strip()
                new_acc[1] += int('{}'.format(name))
                await client.send_message(message.channel, "Added "+" $"+'{}'.format(name)+" To Central Bank")


@client.command(pass_context=True)
async def giveloan(ctx, user:discord.User):
    role = "Bank Manager"
    for r in ctx.message.author.roles:
        if r.name == role:
            await client.send_message(ctx.message.channel, "[Sending loan to {}".format(user.mention)+ "]"+
                                      ": How much? (Type in &add <amount>)")

            def check(msg):
                return msg.content.startswith("&add ")

            message = await client.wait_for_message(author=ctx.message.author, check=check)
            name = message.content[len("&add "):].strip()

            if int(new_acc[int(1)]) < int('{}'.format(name)):
                await client.send_message(message.channel, "Insufficient funds!")
            else:
                new_acc[int(1)] = new_acc[int(1)] - int('{}'.format(name))
                bank_dic[int(user.id)] = bank_dic[int(user.id)] + int('{}'.format(name))
                await client.send_message(message.channel,
                                          "Given " + " $" + '{}'.format(name) + " To {}".format(user.mention))


@client.command(pass_context=True)
async def shoot_burstfire(ctx, user: discord.User):
    await client.send_message(ctx.message.channel, str(ctx.message.author)+" Shot 15 rounds from "+ str(armed_weapons[str(ctx.message.author)] + " at "
                                                                               + "{}".format(user.mention)))

@client.command(pass_context=True)
async def shoot_rapidfire(ctx, user: discord.User):
    await client.send_message(ctx.message.channel, str(ctx.message.author)+ " Shot 30 rounds from "+ str(armed_weapons[str(ctx.message.author)] + " at "
                                                                               + "{}".format(user.mention)))


@client.command(pass_context=True)
async def shoot(ctx, user: discord.User):
    await client.send_message(ctx.message.channel, str(ctx.message.author)+ " Shot 1 round from "+ str(armed_weapons[str(ctx.message.author)])+ " at "
                              + str("{}".format(user.mention)))




@client.command(pass_context=True)
async def give(ctx, user: discord.User):

        await client.send_message(ctx.message.channel, "[Giving credits to {}".format(user.mention) + "]"
                                  +": How much? (Type in &add <amount>)")

        def check(msg):
            return msg.content.startswith("&add ")
        message = await client.wait_for_message(author=ctx.message.author, check=check)
        name = message.content[len("&add "):].strip()

        if int(bank_dic[int(ctx.message.author.id)]) < int('{}'.format(name)):
            await client.send_message(message.channel, "Insufficient credits!")
        else:
            bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] - int('{}'.format(name))
            bank_dic[int(user.id)] = bank_dic[int(user.id)] + int('{}'.format(name))
            await client.send_message(message.channel, "Given "+" $"+'{}'.format(name)+" To {}".format(user.mention))


@client.command(pass_context=True)  
async def open_account(ctx):

    if int(ctx.message.author.id) not in pistol_dic or bank_dic or smg_dic \
            or rifle_dic or tank_dic or plane_dic:
        pistol_dic.update({int(ctx.message.author.id): ""})
        smg_dic.update({int(ctx.message.author.id): ""})
        rifle_dic.update({int(ctx.message.author.id): ""})
        tank_dic.update({int(ctx.message.author.id): ""})
        plane_dic.update({int(ctx.message.author.id): ""})
        bank_dic.update({int(ctx.message.author.id): 0})
        await client.say("Armoury account opened for " + str(ctx.message.author))

    else:
        await client.say("Ops, Looks like you already have an account!")


@client.group(pass_context=True)    
async def balance(ctx,):
    try:
        embed = discord.Embed(title=str(ctx.message.author) + " Your balance is " + "$" +
                                str(bank_dic[int(ctx.message.author.id)]), colour=0xFFFFF)
        return await client.say(embed=embed)
    except:
        await client.say("You do not have an account yet!")


@client.group(pass_context=True)    
async def centralbank(ctx,):
    embed = discord.Embed(title= "Central Bank Balance is"+" $" + str(new_acc[1]), colour=0xFFFFF)
    return await client.say(embed=embed)

#@client.command(pass_context=True)      # Gives people 20 credits every 24 hours
#async def daily(ctx):
#    bank_dic[int(ctx.message.author.id)] = bank_dic[int(ctx.message.author.id)] + 20

client.run(TOKEN HERE)


file1 = open("save_file.py", "w")
file1.write("a2=" + str(bank_dic))
file1.write("\n"+ "a3="+ str(new_acc))  
file1.write("\n"+"a4="+ str(pistol_dic))
file1.write("\n"+"a5="+ str(smg_dic))
file1.write("\n"+"a6="+ str(rifle_dic))
file1.write("\n"+"a7="+ str(tank_dic))
file1.write("\n"+"a8="+ str(plane_dic))
file1.close()
print("saving...")








