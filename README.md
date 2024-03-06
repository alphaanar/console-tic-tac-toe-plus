# Tic Tac Toe Plus
The well-known Tic Tac Toe game with many additional game mechanics written in C for Windows. This project was created for a university assignment.

## Main Idea

In a game as simple as Tic Tac Toe, if you are playing conventionally, there is really not much you can do to add a little bit more fun to gameplay. Originally, we were given a task to create a replica of this game within a week; however, one thing we realized while developing it was that we finished it in just 4 hours. So we decided to add random features to it and call it Tic Tac Toe *Plus*. The first time anyone tries to play, they immediately notice a couple of key differences, such as the way grids and prompts are printed, user input validation, and the great flexibility in almost all game mechanics.

## Launch

The game starts with a little window greeting the player(s). The text slowly fills in and later it asks for a key press. Pressing `Enter` takes the player to the main menu. There is a big sign at the top of the screen displaying the title of the game with a short animation using a "sliding window" effect. Note that we use [box-drawing characters](https://en.wikipedia.org/wiki/Box-drawing_character) extensively.

![Launch](/res/launch.gif)

## Menus & Prompts & Input Validation

All menus generally list all the options and actions you can perform with their brief descriptions. One important nuance here is that the player needs to enter options as plain texts, while some might expect it to listen for key presses. For consistency reasons, we have grouped texts into four categories in terms of their purpose:
 * `#` - Preceeds a comment or a block of info.
 * `>` - Preceeds a prompt and then user input.
 * `!` - Preceeds an error message.
 * `~` - Preceeds a warning message.
This may seem a little confusing *at first*, but overall, this way we can provide more readability.

The program will try to validate every possible user input and print an error message in case of a failure; users can re-enter their input after an error. Inputs are parsed in a case-insensitive manner, i.e. it does not matter whether `a` or `A` is entered. Prompts that require multiple arguments use white-space characters as delimiters (except for newline characters); additionally, all extra characters are trimmed and ignored. Below you can see a list of all options in the main menu (`#`), a prompt for the user (`>`), and a series of error messages for different reasons (`!`):

![Menu](/res/categories-of-texts.png)

## Grid Size

In a conventional Tic Tac Toe, the board is only 3 by 3. Since this is a quite common feature to implement, we decided to have it as well. Entering the option `D` shows the current dimensions of the board and enables you to customize the grid size in any way you want. Entering one integer `n` creates a board of size `n` by `n`, but you can set dimensions separately as well by entering two numbers `n` and `m`. Entering no values applies no changes and simply takes the player back to the menu.

![Resize Grid](/res/resize-grid.png)

## Win Condition

Because now it is possible to have larger grid sizes, it also makes sense to change the winning condition of the game. For instance, in a 6x6 grid, it might be more balanced if the game required 4 of their marks to be placed in a horizontal, vertical, or diagonal row, instead of 3. You cannot set the win condition higher than the minimum of height and width of the board, i.e. `3 <= WIN_CONDITION <= MIN(X, Y)`.

![Win Condition](/res/win-condition.png)
