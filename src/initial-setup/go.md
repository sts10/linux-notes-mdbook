# Go

Go is a board game!

A good desktop app that works for Linux is [Sabaki](https://sabaki.yichuanshen.de/) ([GitHub repo](https://github.com/SabakiHQ/Sabaki)). To install it, I went with the x64 AppImage, probably from [the GitHub Releases tab](https://github.com/SabakiHQ/Sabaki/releases)).

In Sabaki you can play against yourself or load and go through SGF files. But you can also "attach" [a number of "game engines"](https://github.com/SabakiHQ/Sabaki/blob/master/docs/guides/engines.md) to Sabaki to either play against or have analyze games. You can manage the engines available to Sabaki by going to "Engines" > "Manage Engines". 

## Setting up the GNU Go Engine

[GNU Go](https://www.gnu.org/software/gnugo/gnugo.html) is an engine that's nice in that it can (a) play on multiple board sizes out of the box, and (b) has multiple levels to choose from (1 through 10 or 1 through 9, I'm not sure).

### Installing GNU Go on Ubuntu

Go to the [Download page](https://www.gnu.org/software/gnugo/download.html) and download the source code to the latest version of GNU Go. It's likely to be a `tar.gz` file. Once downloaded, expand it. 

Inside that directory, there should be a README and an INSTALL documentation text file for you. But basically, to make the executable for a specific level, I'm pretty sure you run:

```
./configure --enable-level=4; make
```

To build a level 4 binary. (There are plenty of other options explained in one of the documentation text files.) This binary will be created and placed at `./interface/gnugo`. Cool. 

Now in Sabaki, go to Engines > Manage Engines and click the "Add" button. For path, enter `path/to/interface/gnugo`, and then for "arguments" I'm pretty sure you want to put `--mode gtp`. Leave "Initial commands" blank. Note that after Adding an engine, you may need to restart Sabaki to use it.

To build/attach **multiple levels** of GNU Go, I just duplicated the entire `gnudo` directory and rebuilt with the level I want. So in `go-engines` I've got:

```txt
go-engines/gnugo-3.8-lvl1
go-engines/gnugo-3.8-lvl2
go-engines/gnugo-3.8-lvl3
go-engines/gnugo-3.8-lvl5
go-engines/gnugo-3.8-lvl7
go-engines/gnugo-3.8-lvl9
```

each of which have their own executables at `interface/gnugo` to attach in Sabaki. For example, my engine named "GNUGo_lvl_3" has a path of `go-engines/gnugo-3.8-lvl3/interface/gnugo` ("arguments" for all of them are (still) `--mode gtp`).

## Pachi

[Pachi](https://github.com/pasky/pachi) is a pretty strong engine, but that, unlike LeelaZero, can play smaller board sizes out-of-the-box, so to speak. The developers note:

> The default engine plays by Chinese rules and should be about 7d KGS strength on 9x9. On 19x19 it can hold a solid KGS 2d rank on modest hardware (Raspberry Pi, dcnn) or faster machine (e.g. six-way Intel i7) without dcnn.

### Install Pachi via pre-compiled binary
To install Pachi via pre-compiled binary, head over to [GitHub Releases page](https://github.com/pasky/pachi/releases) and download the latest `-linux-static.zip`. Extract this. 

### Connecting Pachi to Sabaki

I didn't change any configurations. 

Then in Sabaki, I just entered the path to the `pachi-12.40-amd64` file in the unzipped directory, with no arguments or initial commands, and it seems to work. However, as I installed it, it can only do analysis on 19x19 boards I think?

### Compiling Pachi from Source

I haven't tried this, but the Pachi README says it might improve performance to build it from source. [Instructions here](https://launchpad.net/~lemonsqueeze/+archive/ubuntu/pachi).

## Setting up LeelaZero (Ubuntu)

1. Download and install [Sabaki](https://github.com/SabakiHQ/Sabaki/). Make sure it runs before proceeding.
2. [Build LeelaZero from source](https://github.com/leela-zero/leela-zero#example-of-compiling---ubuntu--similar)
3. Get a "network hash file" for LeelaZero, "likely the best network is the one you want". [Download it here](http://zero.sjeng.org/best-network) or find [more instructions here](https://github.com/SabakiHQ/Sabaki/blob/master/docs/guides/engines.md).
4. In Sabaki, go to Engines > Manage Engines. Enter the absolute file path to the `leelaz` binary file you just built, which is probably at something like `leela-zero/build/leelaz`. For "Arguments", enter `--gtp -w path/to/weightsfile` (which I think is the "network hash file"?)
5. Restart Sabaki 
6. Find the Game Info menu item. For White, in the drop-down menu, select Leela Zero. Make sure you choose a 19 by 19 board. And you're probably going to want a large handicap.

## How to play against a game engine in Sabaki

To play against one of these engines, open Sabaki. Be sure you're on a blank, new game. Then go to "File" > "Game Info". If you want Balck, make the engine take Whtie by clicking the down arrow next to "White" and selecting the engine you want to play. Fill out the other fields as desired, then hit the OK button. If you're Black, place a stone to start the game, and the engine should respond. To see what the engine is doing, go to "Engines" > "Toggle GTP console".

Alternatively you can manually attach an engine by going to Engines > "Attach". 

## Recommended Sabaki preferences

To prevent engines from making moves _right_ when you initially attach them (which can be annoying if you just want to use the engine to analyze possible moves [see below]), I would go to File > Preferences and uncheck "Start game right after attaching engines". The con to this is that to start playing a game against an engine, you have to first attach it ("Engines" > "Attach"), then (sometimes) tell it to start playing ("Engines" > "Start Playing").

## Using a game engine to do analysis of a game in Sabaki

Some of these engines  -- like LeelaZero and Pachi -- allow you to analyze next moves (though usually only on 19x19 games it seems?). To do this:

1. "Engines" > "Toggle Analysis" gives you a heat map of what the engine likes for the next move. Leela will do both show the analysis of its moves _as well as_ provide analysis for your move (you can accept by clicking on the green blob, or move somewhere else)
2. With "Analysis" toggled on, you can also hover a piece over a space and the engine will play out the game from there, if you were to move there.

If the GPU load gets to be too much, you can always make the engine suspend by going to "Engines" > "Suspend". Toggling Analysis off will help too, as the engine won't think during your move.
