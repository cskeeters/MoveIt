# MoveIt

MoveIt is a macOS Window Mover/Resizer (some would say *Manager*) built on top of [Hammerspoon](https://www.hammerspoon.org/) ([github](https://github.com/Hammerspoon/hammerspoon)).  This operates similarly to [Spectical](https://www.spectacleapp.com/) or [Rectangle](https://rectangleapp.com/).

This program is a modification of [ShiftIt](https://github.com/peterklijn/hammerspoon-shiftit) with functionality customized according to my preferences.  With Hammerspoon doing all of the hard work, you may want to customize MoveIt or ShiftIt to meet your needs rather than use either of these tools as is.  The code is just one init.lua file, and it's not that many lines of code.

## Hammerspoon Background

Hammerspoon is a program that allows developers to interact with macOS via lua.  Hammerspoon is a program that runs in the background with an icon in the menu bar.  Out of the box, it does nothing, but users can add and configure *spoons* that enable various functionality.  This project offers one such spoon.

Hammerspoon's configuration exists in `~/.hammerspoon/init.lua`.  If you install spoons, they will be installed in `~/.hammerspoon/Spoons/`.  A spoon is essentially a folder with an `init.lua` file in it.  Hammerspoon configures finder to see folders with a suffix of `.spoon` as a package and sets Hammerspoon as the associated program to load this package.  If you double click on a spoon, it will move that folder into `~/.hammerspoon/Spoons/`.  This is one way to install a Spoon.  Another is to simply create the folders you need and copy the init.lua file inside.  A third way is to use SpoonInstall which reminds me of a vim plugin manager.

## Installing MoveIt

Step 1: Install HammerSpoon.  Get a zip file from <https://github.com/Hammerspoon/hammerspoon/releases/>, unzip it and move the Hammerspoon.app into `/Applications`.

Step 2: Enable the application to run.  `Hammerspoon.app` is not signed so it will not run without explicitly allowing it to run.  See <https://support.apple.com/en-us/HT202491>  The easiest way is to 
1. Try and run the program, let it fail
2. Open up *System Settings*
3. Click on *Privacy & Security*, 
4. Scroll down to the bottom and find the **Open Anyway** button.

Step 3: Run Hammerspoon.

Step 4: Enable Notifications.  Notifications are not enabled by default, a spoon may want to communicate with you via notifications.  To enable notifications:
1. Open up *System Settings*
2. Click on *Notifications* 
3. Click on Hammerspoon
4. Enable **Allow notifications**

Step 5: Install MoveIt.

1. Open *Terminal* or your favorite terminal application.
2. Run the following commands

```bash
cd ~/.hammerspoon
mkdir -p Spoons
cd Spoons
```

3. Run 

```bash
git clone git@github.com:cskeeters/MoveIt.git MoveIt.spoon
```

**or**

```bash
mkdir MoveIt.spoon
cd MoveIt.spoon
curl http://github.com/cskeeters/MoveIt/init.lua --output init.lua
```

4. Configure Hammerspoon to run the spoon.  Edit `~/.hammerspoon/init.lua` and insert the following.

```lua
local moveIt = hs.loadSpoon("MoveIt")
-- change keys here
-- moveIt.mash = { 'ctrl', 'cmd' }
-- moveIt.centerKey = 'c'
-- ...
moveIt:init()
```

## Usage

The defining feature of MoveIt is that each action has multiple states.  Press the keybinding repeatedly to cycle through the states.  This limits the amount of keys to remember for a bit greater functionality.  The default keybindings are made so that your hands don't move from the home row much.

By default all keybindings require three modifiers: ^+⌥+⌘.  With these modifiers pressed, the following keys will take the listed actions.

NOTE: This table is a bit weird but helps see the relative location of the keys.

key/action | key/action | key/action
-----------|------------|----------
u/upLeft   | i/up       | o/upRight
j/left     | k/center   | l/right
m/downLeft | k/down     | l/downRight

key       | action
----------|----------
return    | fullscreen
n         | nextScreen
p         | prevScreen


Action     | State 0                                                   | State 1
-----------|-----------------------------------------------------------|---------------------------------------------------------
up         | Move/Resize the window to the upper half    of the screen | Move/Resize the window to the upper 2/3rds of the screen
down       | Move/Resize the window to the lower half    of the screen | Move/Resize the window to the lower 2/3rds of the screen
left       | Move/Resize the window to the  left half    of the screen | Move/Resize the window to the left  2/3rds of the screen
right      | Move/Resize the window to the right half    of the screen | Move/Resize the window to the right 2/3rds of the screen
upLeft     | Move/Resize the window to the upper-left    of the screen | N/A (Only one state)
upRight    | Move/Resize the window to the upper-right   of the screen | N/A (Only one state)
downLeft   | Move/Resize the window to the lower-left    of the screen | N/A (Only one state)
downRight  | Move/Resize the window to the lower-right   of the screen | N/A (Only one state)
fullscreen | Move/Resize the window to the middle 2/3rds of the screen | Move/Resize the window to the entire screen
nextscreen | Move the window to the next screen                        | N/A (Only one state)
prevscreen | Move the window to the previous screen                    | N/A (Only one state)
