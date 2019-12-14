# Go

A good desktop app: [Sabaki](https://sabaki.yichuanshen.de/ ([GitHub](https://github.com/SabakiHQ/Sabaki)). To install it, I went with the x64 AppImage, probably from [the GitHub Releases tab](https://github.com/SabakiHQ/Sabaki/releases)).

## Setting up LeelaZero (Ubuntu)

1. Download and install [Sabaki](https://github.com/SabakiHQ/Sabaki/). Make sure it runs before proceeding.
2. [Build LeelaZero from source](https://github.com/leela-zero/leela-zero#example-of-compiling---ubuntu--similar)
3. Get a "network hash file" for LeelaZero, "likely the best network is the one you want". [Download it here](http://zero.sjeng.org/best-network) or find [more instructions here](https://github.com/SabakiHQ/Sabaki/blob/master/docs/guides/engines.md).
4. In Sabaki, go to Engines > Manage Engines. Enter the absolute file path to the `leelaz` binary file you just built, which is probably at something like `leela-zero/build/leelaz`. For "Arguments", enter `--gtp -w path/to/weightsfile` (which I think is the "network hash file"?)
5. Restart Sabaki 
6. Find the Game Info menu item. For White, in the drop-down menu, select Leela Zero. Make sure you choose a 19 by 19 board. And you're probably going to want a large handicap.

## Cool things you can do now that you have an engine attached

1. "Engines" > "Toggle Analysis" gives you a heat map of what Leela likes for the next move. Leela will do both show the analysis of its moves _as well as_ provide analysis for your move (you can accept by clicking on the green blob, or move somewhere else)
2. With "Analysis" toggled on, you can also hover a piece over a space and Leela will play out the game from there, if you were to move there.

If the GPU load gets to be too much, you can always make Leela suspend by going to "Engines" > "Suspend". Toggling Analysis off will help too, as Leela won't think during your move.


