# Every Scoreboard

A tool to generate all the scoreboard objectives available in Minecraft.
All of them, for ~~any~~ most versions.

It works by generating a datapack which will create the scoreboards for you.

# How to use

You can find 'pre-made' datapacks over [here](https://github.com/Syntro42/every-scoreboard/tags).
If you don't find what you need, read the following section; you can skip it otherwise.

## 'Compiling'

First of all, clone the repository:
```shell script
$ git clone https://github.com/Syntro42/every-scoreboard.git
$ cd every-scoreboard
```

Install the dependencies with this command;
make sure you have [pip](https://pip.pypa.io/en/stable/installing/) installed.
```shell script
$ pip install -r requirements.txt
```

To 'compile' the datapacks, run the following:
```shell script
$ python3 scripts/create.py --mcversion="1.19" -c
```
The `-c` flag will add the [custom objectives](https://minecraft.gamepedia.com/Statistics#List_of_custom_statistic_names)
to the datapack. Be careful however! It is made for the latest version(s) of the game only.
You will probably need to modify the resulting `mcfunction` files at the end if you
do it for an older version of Minecraft.

The `-eta` flag will add all the block tag objectives from the [EndTech Additions Mod](https://github.com/samipourquoi/endtech-additions)
as well as the [custom objectives](https://minecraft.gamepedia.com/Statistics#List_of_custom_statistic_names). You need EndTech Additions
running on your server for these objectives to work.

The resulting files will end up at `datapacks/every-scoreboard-<version>` and `dictionaries/dictionary-<version>.json`.
We will come back to the second file later on.

## Running the datapack

Once you have the datapack ready, move it over your world's datapacks folder. Log on to your world and enter the following commands:
```
/reload
/function every-scoreboard:create
```

And here you're all set! If you wish to get rid of all of these objectives, run:
```
/function every-scoreboard:delete
```

See the naming convention over in the next section.

Note that the scoreboard names won't change between versions of the game.
That means you can have your world in 1.18 with that datapack, then update your world to 1.19, run the datapack
for that version again, and you will keep your scoreboards from 1.18, with the new ones.

## Naming convention

The scoreboards are name accordingly:
- `m-<block>` Mined blocks
- `u-<item>` Used items
- `c-<item>` Crafted items
- `b-<item>` Broken tools
- `p-<item>` Picked up items
- `d-<item>` Dropped items
- `k-<mob>` Killed mobs
- `kb-<mob>` Killed by mob
- `z-<stats>` Custom (find all the possible `stats` over [here](https://minecraft.gamepedia.com/Statistics#List_of_custom_statistic_names))

# 'Recover' your old stats

What if you have already started your world without all of these fancy scoreboards? No problem!
You can actually take the statistics from your world and convert them to commands, which will update the
objectives to their actual value.

To do so, run the `update.py` script like so:
```shell script
$ python3 scripts/update.py -D="./dictionaries/dictionary-1.19.json" -S="path/to/stats"
```

- the `-D` flag will set the path of the dictionary (needed to convert full name scoreboards to their truncated form).
- the `-S` flag will set the path of the stats folder. It's usually found at `.minecraft/saves/<world>/stats`, or
`<server>/world/stats`. It should contain plenty of JSON files.

There are 5 __optional__ tags. If you have a custom scoreboard made for digs, you can set their name and they will get updated:
- `--dig="<name>"` sets the name of the general dig scoreboard (counts all blocks mined)
- `--picks="<name>"` sets the name of all type pick uses (netherite, diamond, iron...)
- `--shovels="<name>"` sets the name of all type shovel uses
- `--axes="<name>"` sets the name of all type axe uses
- `--hoes="<name>"` sets the name of all type hoe uses

The program will generate a datapack at `datapacks/every-scoreboard-<version>`. Make sure you have a backup of your
world *just in case* something goes wrong. Drag it to your world's datapacks folder,
and enter these commands:
```
/reload
/function #every-scoreboard:update
```

# Credits
The original creator is [`samipourquoi`](https://github.com/samipourquoi) \
I am now the maintainer of this project. You can contact me on Discord `Syntro#9454` \
or via the EndTech discord: https://discord.gg/m6zdS2Pm2J

Feel free to contact me if you need any help 😀
