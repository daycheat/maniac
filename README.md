<h2 align="center">maniac</h2>

<p align="center">Cheating in osu!mania.</p>

This is a very simple external cheat for the game [osu!](https://osu.ppy.sh/), more specifically for the [osu!mania](https://osu.ppy.sh/help/wiki/Game_Modes/osu!mania) gamemode (where this project also got its name from).

It attemps to be
- __simple__ to use through automation and reasonable defaults
- __lightweight__, in the sense that the binaries are small and fast
- __portable__ by offering binaries with equal functionality for Windows and many Linux distributions (where it depends on the X Window System)

```
  Usage: maniac [options]

  Options:

    -p         id of game process (optional)
    -l         humanization level (default: 0)
    -a         address to read time from (optional)
    -m         path to beatmap (optional)
    -r         replay humanization level delta (optional)
    -e         toggle exit checks in game loop (default: on)
    -h         print this message

```

### Humanization

_Please note that this is very far from actual and effective humanization. This feature is in an early alpha stage at best._

The switch `-l` allows the passing of a range in which hitpoint time offsets will be generated.

For further fine-tuning, refer to the `#define RNG_*` defines and the comments of the number generation function in `beatmap.c`.

### Map fetching

If no `-m` switch is passed, `maniac` will attempt to read the beatmap from the window title, and idle while you're in the menus.

Beatmaps are read from the `DEFAULT_OSU_PATH` defined in `osu.h`, and it is assumed that the folder structure has not been tampered with (eg that `Songs/` contains only folders, etc).

The default osu! path on Windows is `C:\Users\<username>\AppData\local\osu!\Songs`, and on Linux it's `/home/<username>/osufolder/Songs`. Since you will likely have gone through some hoops to get osu! running on Linux, it's probably easiest to just symlink `~/osufolder` to wherever you keep your osu! files.

### Replay functionality

The `-r` switch enables replays. After the end of the current map has been reached, `maniac` will restart the current map and play it again.

To (very crudely) simulate human progression, `-r` accepts a value which will be subtracted from the current humanization level at every replay.

## Usage

1. Download the latest build for your operating system by navigating to [releases](https://github.com/LW2904/maniac/releases) and selecting the appropiate executable. Builds postfixed with `debug` have significantly more verbose logging than regular builds but are do not perform as well as a result. They are useful to track down bugs that are hard to reproduce -- when opening an issue please include the output of the debug build.

2. Open your terminal. On Windows this most commonly means running opening the default Command Prompt, which can be done by pressing the Windows button, typing `cmd` and pressing enter.

3. In your terminal, run the executable you just downloaded.
```bash
cd Downloads    # or cd wherever/you/downloaded/it/to
maniac-...      # the full name of the executable goes here, on Linux prefix with ./
                # note that pressing tab will usually autocomplete lines
```

## Building from Source

On Linux, requires you to do `apt install build-essential libxtst-dev libx11-dev`. On Windows, requires `mingw-w64` and `cmake`.

```bash
git clone https://github.com/LW2904/maniac.git
cd maniac
mkdir build && cd build
cmake .. -DCMAKE_SH="CMAKE_SH-NOTFOUND" -DCMAKE_BUILD_TYPE="Debug" ; or "Release"
make ; or mingw32-make, on Windows
```
