![Kaguya](https://telegra.ph/file/9f44458a5f632dcb8c0a5.jpg)
# Kaguya // @KaguyaRobot

[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)
[![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://GitHub.com/Skuzzy_xD/)</br>


![Python Version](https://img.shields.io/badge/python-3.8-green?style=for-the-badge&logo=appveyor)
![Issues](https://img.shields.io/github/issues/Anomaliii/Kaguya?style=for-the-badge&logo=appveyor)
![Forks](https://img.shields.io/github/forks/Anomaliii/Kaguya?style=for-the-badge&logo=appveyor)
![Stars](https://img.shields.io/github/stars/Anomaliii/Kaguya?style=for-the-badge&logo=appveyor)
![LICENSE](https://img.shields.io/github/license/Anomaliii/Kaguya?style=for-the-badge&logo=appveyor)
![Contributors](https://img.shields.io/github/contributors/Anomaliii/Kaguya?style=for-the-badge&logo=appveyor)
![Repository Size](https://img.shields.io/github/repo-size/Anomaliii/Kaguya?style=for-the-badge&logo=appveyor)</br>


[![Join Support!](https://img.shields.io/badge/Support%20Chat-ZeroUnion-red)](https://t.me/ZeroBotSupport) 
[![Codacy Badge](https://app.codacy.com/project/badge/Grade/cfb691a93a064d9ea753ef2b5fccf797)](https://www.codacy.com/manual/Anomaliii/Kaguya?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Anomaliii/Kaguya&amp;utm_campaign=Badge_Grade)


A modular telegram Python bot running on python3 with an sqlalchemy database.

Originally a marie fork - Kaguya has evolved further and was built to be more useful for Anime Chats. 

Can be found on telegram as [Kaguya](https://t.me/ShinomiyaRobot).

The Support group can be reached out to at [Zero Union](https://t.me/ZeroBotSupport), where you can ask for help setting up your bot, discover/request new features, report bugs, and stay in the loop whenever a new update is available. 

 

## Setting up the bot (Read this before trying to use!):


# How to setup
Note: This instruction set is just a copy paste from marie, note that [Zero Union](https://t.me/ZeroBotSupport) aims to handle support for @Kaguyarobot and now how to setup your own fork, if you find this bit confusing/tough to understand then we recommend you ask a dev, kindly avoid asking how to setup the bot instance in the support chat, it aims to help our own instance of the bot. 
  
## Setting up the bot (Read this before trying to use!):
Please make sure to use python3.6, as I cannot guarantee everything will work as expected on older python versions!
This is because markdown parsing is done by iterating through a dict, which are ordered by default in 3.6.

  ### Configuration

   copy sample_config.ini and make a config.ini, satisfy the values in it.


 - `TOKEN`: Your bot token, as a string.
 - `OWNER_ID`: An integer of consisting of your owner ID
 - `OWNER_USERNAME`: Your username

 - `DATABASE_URL`: Your database URL
 - `MESSAGE_DUMP`: optional: a chat where your replied saved messages are stored, to stop people deleting their old 
 - `LOAD`: Space separated list of modules you would like to load
 - `NO_LOAD`: Space separated list of modules you would like NOT to load
 - `WEBHOOK`: Setting this to ANYTHING will enable webhooks when in env mode
 messages
 - `URL`: The URL your webhook should connect to (only needed for webhook mode)

 - `SUDO_USERS`: A space separated list of user_ids which should be considered sudo users
 - `SUPPORT_USERS`: A space separated list of user_ids which should be considered support users (can gban/ungban,
 nothing else)
 - `WHITELIST_USERS`: A space separated list of user_ids which should be considered whitelisted - they can't be banned.
 - `DONATION_LINK`: Optional: link where you would like to receive donations.
 - `CERT_PATH`: Path to your webhook certificate
 - `PORT`: Port to use for your webhooks
 - `DEL_CMDS`: Whether to delete commands from users which don't have rights to use that command
 - `STRICT_GBAN`: Enforce gbans across new groups as well as old groups. When a gbanned user talks, he will be banned.
 - `WORKERS`: Number of threads to use. 8 is the recommended (and default) amount, but your experience may vary.
 __Note__ that going crazy with more threads wont necessarily speed up your bot, given the large amount of sql data 
 accesses, and the way python asynchronous calls work.
 - `BAN_STICKER`: Which sticker to use when banning people.
 - `ALLOW_EXCL`: Whether to allow using exclamation marks ! for commands as well as /.

  ### Python dependencies

Install the necessary python dependencies by moving to the project directory and running:

`pip3 install -r requirements.txt`.

This will install all necessary python packages.

  ### Database

If you wish to use a database-dependent module (eg: locks, notes, userinfo, users, filters, welcomes),
you'll need to have a database installed on your system. I use postgres, so I recommend using it for optimal compatibility.

In the case of postgres, this is how you would set up a the database on a debian/ubuntu system. Other distributions may vary.

- install postgresql:

`sudo apt-get update && sudo apt-get install postgresql`

- change to the postgres user:

`sudo su - postgres`

- create a new database user (change YOUR_USER appropriately):

`createuser -P -s -e YOUR_USER`

This will be followed by you needing to input your password.

- create a new database table:

`createdb -O YOUR_USER YOUR_DB_NAME`

Change YOUR_USER and YOUR_DB_NAME appropriately.

- finally:

`psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

This will allow you to connect to your database via your terminal.
By default, YOUR_HOST should be 0.0.0.0:5432.

You should now be able to build your database URI. This will be:

`sqldbtype://username:pw@hostname:port/db_name`

Replace sqldbtype with whichever db youre using (eg postgres, mysql, sqllite, etc)
repeat for your username, password, hostname (localhost?), port (5432?), and db name.

  ## Modules
   ### Setting load order.

The module load order can be changed via the `LOAD` and `NO_LOAD` configuration settings.
These should both represent lists.

If `LOAD` is an empty list, all modules in `modules/` will be selected for loading by default.

If `NO_LOAD` is not present, or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

   ### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file be in the modules folder.

To add commands, make sure to import the dispatcher via

`from tg_bot import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user
friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so 
it is necessary to migrate it in the db.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed 
through the `/stats` command, which is only available to the bot owner.

## Starting the bot.

Once you've setup your database and your configuration is complete, simply run the bat file(if on windows) or run (linux):

`python3 -m tg_bot`

You can use [nssm](https://nssm.cc/usage) to install the bot as service on windows and set it to restart on /gitpull 
Make sure to edit the start and restart bats to your needs. 
Note: the restart bat requires that User account control be disabled.


For queries or any issues regarding the bot please open an issue ticket or visit us at [Zero Union](https://t.me/ZeroBotSupport)  
</details>  

## Credits
The bot is based of on the original work done by [PaulSonOfLars](https://github.com/PaulSonOfLars)
This repo was just reamped to suit an Anime-centric community. All original credits go to Paul and his dedication, Without his efforts, this fork would not have been possible!

And big thanks to [Dank - del](https://github.com/Dank-del) to make [Kigyō](https://github.com/Dank-del/EnterpriseALRobot) for base and inspiring me make this bot.

Also, missing proper credit for blacklistusers taken from TheRealPhoenixBot (will add it later, this note says unless its done)

Any other authorship/credits can be seen through the commits.


Should any be missing kindly let us know at [Zero Union](https://t.me/ZeroBotSupport) or simply submit a pull request on the readme.

## © Zero Union (2021)
 Software licensed under GPLv3
