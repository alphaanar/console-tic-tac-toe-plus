# Tic Tac Toe Plus
The well-known Tic Tac Toe game with many additional game mechanics written in C for Windows. This project was created for a university assignment.

## Main Idea

In a game as simple as Tic Tac Toe, if you are playing conventionally, there is really not much you can do to add a little bit more fun to gameplay. Originally, we were given a task to create a replica of this game within a week; however, one thing we realized while developing it was that we finished it in just 4 hours. So we decided to add random features to it and call it Tic Tac Toe *Plus*. The first time anyone tries to play, they immediately notice a couple of key differences, such as the way grids and prompts are printed, user input validation, and the great flexibility in almost all game mechanics.

## Launch

The game starts with a little window greeting the player(s). The text slowly fills in and later it asks for a key press. Pressing `Enter` takes the player to the main menu. A big sign at the top of the screen displays the title of the game with a short animation using a "sliding window" effect. Note that we use [box-drawing characters](https://en.wikipedia.org/wiki/Box-drawing_character) extensively.

---
![Launch](/res/launch.gif)
---

## Menus & Prompts & Input Validation

All menus generally list all the options and actions you can perform with their brief descriptions. One important nuance here is that the player needs to enter options as plain texts, while some might expect it to listen for key presses. For consistency reasons, we have grouped texts into four categories in terms of their purpose:

* `#` - Preceeds a comment or a block of info.
* `>` - Preceeds a prompt and then user input.
* `!` - Preceeds an error message.
* `~` - Preceeds a warning message.

This may seem a little confusing *at first*, but overall, this way we can provide more readability.

The program will try to validate every possible user input and print an error message in case of a failure; users can re-enter their input after an error. Inputs are parsed case-insensitively, i.e. it does not matter whether `a` or `A` is entered. Prompts that require multiple arguments use white-space characters as delimiters (except for newline characters); additionally, all extra characters are trimmed and ignored. Below you can see a list of all options in the main menu (`#`), a prompt for the user (`>`), and a series of error messages for different reasons (`!`):

---
![Menu](/res/categories-of-texts.png)
---

## Grid Size

In a conventional Tic Tac Toe, the board is only 3 by 3. Since this is a quite common feature to implement, we decided to have it as well. Entering the option `D` shows the current dimensions of the board and enables you to customize the grid size in any way you want. Entering one integer `n` creates a board of size `n` by `n`, but you can set dimensions separately as well by entering two numbers `n` and `m`. Entering no values applies no changes and simply takes the player back to the menu.

---
![Grid Size](/res/resize-grid.png)
---

## Win Condition

Because now it is possible to have larger grid sizes, it also makes sense to change the winning condition of the game. For instance, in a 6x6 grid, it might be more balanced if the game required 4 of their marks to be placed in a horizontal, vertical, or diagonal row, instead of 3. You cannot set the win condition higher than the minimum of height and width of the board, i.e. `3 <= WIN_CONDITION <= MIN(X, Y)`. If you first set the win condition and then the grid size, the game automatically adjusts the settings.

---
![Win Condition](/res/win-condition.png)
---

## Player Count

What a surprise, you can also play with more than two players; the option for that is `N`. The formula for the maximum number of allowable players is slightly more complicated: `2 <= PLAYER_COUNT <= MIN(10, (X * Y - 1) / (WIN_CONDITION - 1) - 1)`. But we should not worry about the derivation of this formula, the game does everything for us in order to ensure that the grid is large enough for at least one player to win.

## Player Symbols

In the original game, we had `X` and `O` to represent two players, but with the greater number of players, all of them must have a unique associative symbol. By default, the game chooses the following symbols to represent players from 1 to 10: [`X`, `O`, `Y`, `Z`, `A`, `B`, `C`, `D`, `E`, `F`]. However, there is another option `S` with which players can replace existing symbols in use with another symbol from `A` to `Z` (all uppercase) as they wish. If you replace a symbol with another symbol that is already used, the game swaps their order to avoid duplicates.

---
![Player Symbols](/res/player-symbols.png)
---

## Miscellaneous

Options `M` and `C` are used in order to switch the theme and clear the console. Switching the theme might sound fancy but all it does is to invert the colors of the console so that white appears black and vice versa. Clearing the console can be useful when there are too many logged texts or error messages on the screen and you want to get rid of clutter.

## Gameplay

After entering the option `P`, the game will immediately start and a bunch of things will appear on the screen:
1. Win condition & Move count: This is to remind players how many identical symbols in a row count as a win and how many moves overall were performed.
2. List of auxiliary actions:
    * In cases of mishap, you can enter `Z` to undo the most recent moves until the move count reaches 0 again.
    * Whenever a match is to end in a tie and there is no point in continuing, players can choose to declare a tie earlier with the option `T`.
    * The option `Q` is for quitting the match, either because the game settings were not right or because everyone got bored.
3. The game board: An `n` by `m` grid labeled from all four sides with zero-based coordinates displaying all moves by the players using their symbols.
4. Player list: This list contains all players' symbols and shows whose turn it is with a rotating indicator.
5. Input line: Players can enter either the coordinates of a new move or one of the options for auxiliary actions.

When a player enters the coordinates that they want to mark, the corresponding cell on the grid will be annotated with `#` at first. At this point, the game awaits a confirmation from the player that this is the cell they indeed want to choose. To confirm a move, players need to enter blank again, and only then the cell with `#` on the grid will be shown as the player's symbol. However, instead of confirming the move, the player can also re-enter other coordinates to place `#` on another cell if they made a typo or changed their mind.

---
![Gameplay](/res/gameplay.png)
---
![Gameplay](/res/confirm-selection.png)
---
![Gameplay](/res/victory.png)
---

## Game Modes

## Quit

Enter option `Q` from the main menu to exit the game. :)

---
![Quit](/res/quit.png)
---
