
# Table of Contents

1.  [Objective](#org45f8a0d)
2.  [With Python](#org184aae4)
    1.  [Planning](#orgc47739c)
        1.  [Requirements](#orgcd6823a)
        2.  [Functions](#org49b5308)
    2.  [Implementation](#org5db8a52)
        1.  [Board in a dictionary form](#orgf89361e)
        2.  [Printing the board](#org4626278)
        3.  [Asking the user to make a move](#org633a59f)
        4.  [Making the move of the user in the table](#org0c0e5bc)
        5.  [Changing player's turn](#orgc4218ea)
        6.  [Knowing whether to continue the game](#org006a75f)
        7.  [The main function](#org6456a47)



<a id="org45f8a0d"></a>

# Objective

Create a program to play tic tac toe


<a id="org184aae4"></a>

# With Python

With python I will drive this project as a cli game. I will use a [dictionary](20250111130125-python_dictionary.md) to save the state of the board.


<a id="orgc47739c"></a>

## Planning


<a id="orgcd6823a"></a>

### Requirements

-   Receive a movement command from the players
-   Update the table state accordingly
-   Automatic updating the turns, the game will automatically know which player's turns is.
-   Know when the game ends:
    -   There is a winner
    -   The board is full


<a id="org49b5308"></a>

### Functions

-   **ask<sub>move</sub>(player)**: This function will ask the movement for the player
-   **make<sub>mov</sub>(move, board, player)**: This function will update the board
-   **change<sub>player</sub>(player)**: This function will change the player.
-   **continue<sub>game</sub>(board)**: This function will determine if the game continue with the help of this function:
    -   **check<sub>winner</sub>(board, scenario)**: This function check if there is a winner by checking if the board has any of the winner cases.


<a id="org5db8a52"></a>

## Implementation


<a id="orgf89361e"></a>

### Board in a dictionary form

To represent the board with a dictionaty I will declare the nine positions with the following keys:
"top<sub>L</sub>": Top Left
"top<sub>M</sub>": Top Mid
"top<sub>R</sub>": Top Right
"mid<sub>L</sub>": Mid Left
"mid<sub>M</sub>": Mid Mid
"mid<sub>R</sub>": Mid Right
"bot<sub>L</sub>":  Bot Left
"bot<sub>M</sub>":  Bot Mid
"bot<sub>R</sub>":  Bot Right

I will initialize each key with the value "". So this will be the initial dictionary for board
\#+begin<sub>src</sub> python
board = {
    'top<sub>L</sub>': "", 'top<sub>M</sub>': "", 'top<sub>R</sub>': "",
    'mid<sub>L</sub>': "", 'mid<sub>M</sub>': "", 'mid<sub>R</sub>': "",
    'bot<sub>L</sub>': "", 'bot<sub>M</sub>': "", 'bot<sub>R</sub>': "",
}
\#+end<sub>src</sub>>


<a id="org4626278"></a>

### Printing the board

The first thing that I notice is that I will need some function to print the board, because I need it to be printed in each iteration of the game loop and at the end, so in order to not repeat myself I will need a function for this work. Therefore, I created the next functions:

    def print_board_square(board, position):
        if (board[position] == ""):
            print(" |", end="")
        else:
            print(f"{board[position]}|", end="")
    
    def print_board(board):
        print("\n")
        print_board_square(board, 'top_L')
        print_board_square(board, 'top_M')
        print(board['top_R'])
        print("-+-+-")
        print_board_square(board, 'mid_L')
        print_board_square(board, 'mid_M')
        print(board['mid_R'])
        print("-+-+-")
        print_board_square(board, 'bot_L')
        print_board_square(board, 'bot_M')
        print(board['bot_R'])

The first function `print_board_square(board, position)` it's just a helper cause I dont wanted to write the block of code in charge to print " " when the position in the board was empty. Another way, a easier one would have be initialize the dicitonary with the value of " " instead of "".


<a id="org633a59f"></a>

### Asking the user to make a move

For this, I will present the user with a menu of the commands that he has available to make a move and then I will return his entry in lowercase.
\#+begin<sub>src</sub> python
def ask<sub>mov</sub>(player):
    print("\ntl: Top Left")
    print("tm: Top Mid")
    print("tr: Top Right")
    print("ml: Mid Left")
    print("mm: Mid Mid")
    print("mr: Mid Right")
    print("bl: Bot Left")
    print("bm: Bot Mid")
    print("br: Bot Right\n")

    print(f"\nIt's turn of {player}'s")
    move = input("Give the position for your movement: ").lower()
    return move
\#+end<sub>src</sub>>


<a id="org0c0e5bc"></a>

### Making the move of the user in the table

For this I will use another dictionary to "translate" the command that the user gave to a key of the board. To make a move I have to check if the given command is valid and if the position is valid. The first thing is just a verification if "move" is in "movements.keys()", the second one is verifying if the position is empty. This function have to return some control value in order to know if I have to change the player or no. This is the code:

    def make_mov(move, board, player):
        movements = {
            "tl": 'top_L',
            "tm": 'top_M',
            "tr": 'top_R',
            "ml": 'mid_L',
            "mm": 'mid_M',
            "mr": 'mid_R',
            "bl": 'bot_L',
            "bm": 'bot_M',
            "br": 'bot_R',
        }
    
        if move not in movements.keys():
            print("Invalid Position")
            return 1
    
        board_dir = movements[move]
    
        if board[board_dir] != "":
            print("\nInvalid movement: Position already taken, you lose a turn for fool")
        else:
            board[board_dir] = player
    
        return 0


<a id="orgc4218ea"></a>

### Changing player's turn

I will have a variable which will change accordingly to the turns. For example: if it is x's turn this variable will have the value "x". However, if it is o's turns, this variable will have the value "o". Therefore to change the turn I just have to change this value, that's way this function just receive this variable and return another value accordingly. This is the code:

    def change_player(player):
        if player=='o':
            player='x'
        else:
            player='o'
    
        return player


<a id="org006a75f"></a>

### Knowing whether to continue the game

I will need two functions for this requirement:

1.  Will check if there is a winner
2.  Will check if the board is full or there is a winner
    The first one is an auxiliar one. The way I solve this problem of knowing whether there is a winner is by listing the winner cases in the tic-tac-toe, the winner cases are the one in which three specific positions have the same value if this value is different from the initial value. Therfore, I create the following [list](20250111131854-python_list.md)  inside the second function.
    
        win_scenarios = [
            ('top_L', 'top_M', 'top_R'),
            ('mid_L', 'mid_M', 'mid_R'),
            ('bot_L', 'bot_M', 'bot_R'),
            ('top_L', 'mid_L', 'bot_L'),
            ('top_M', 'mid_M', 'bot_M'), 
            ('top_R', 'mid_R', 'bot_R'),
            ('top_R', 'mid_M', 'bot_L'),
            ('top_L', 'mid_M', 'bot_R'),
        ]

This is a list of [tuples](20250114030727-python_tuples.md) that represents the winner cases. In the function that checks if there is a winner, I receive one of these scenarios and compare if the position of the scenarios have all three of them the same value in the board.
The `check_winner` function looks like this

    def check_winner(board, scenario):
        return board[scenario[0]] == board[scenario[1]] == board[scenario[2]] != ""

And the `continue_game` function looks like this
\#+begin<sub>src</sub> python
def continue<sub>game</sub>(board):
    win<sub>scenarios</sub> = [
        ('top<sub>L</sub>', 'top<sub>M</sub>', 'top<sub>R</sub>'),
        ('mid<sub>L</sub>', 'mid<sub>M</sub>', 'mid<sub>R</sub>'),
        ('bot<sub>L</sub>', 'bot<sub>M</sub>', 'bot<sub>R</sub>'),
        ('top<sub>L</sub>', 'mid<sub>L</sub>', 'bot<sub>L</sub>'),
        ('top<sub>M</sub>', 'mid<sub>M</sub>', 'bot<sub>M</sub>'), 
        ('top<sub>R</sub>', 'mid<sub>R</sub>', 'bot<sub>R</sub>'),
        ('top<sub>R</sub>', 'mid<sub>M</sub>', 'bot<sub>L</sub>'),
        ('top<sub>L</sub>', 'mid<sub>M</sub>', 'bot<sub>R</sub>'),
    ]
    there<sub>is</sub><sub>winner</sub> = any(check<sub>winner</sub>(board, scenario) for scenario in win<sub>scenarios</sub>)
    is<sub>full</sub> = not any(v=="" for v in board.values())

if(there<sub>is</sub><sub>winner</sub>):
    print(f"\nGanador: {board['top<sub>L</sub>']}")
elif is<sub>full</sub>:
    print("It's a tie")

    return not (there<sub>is</sub><sub>winner</sub> or is<sub>full</sub>)
\#+end<sub>src</sub>>
As it can be seen, I use the [any()](20250114030832-python_any.md) function which essentially returns true if any of the cases passed are true. I use this function to get the `there_is_winner` variable and the `is_full` variable. I have to explai the obtaintion of the `is_full` variable. It just iterate the board and look if there is a "" value, because if there is such value it indicates the board is not empty so I need the `any()` function to return false to it be true, so I use the `not` operator.


<a id="org6456a47"></a>

### The main function

Lastly the main function is this:
\#+begin<sub>src</sub> python
def main():
    board = {
        'top<sub>L</sub>': "", 'top<sub>M</sub>': "", 'top<sub>R</sub>': "",
        'mid<sub>L</sub>': "", 'mid<sub>M</sub>': "", 'mid<sub>R</sub>': "",
        'bot<sub>L</sub>': "", 'bot<sub>M</sub>': "", 'bot<sub>R</sub>': "",
    }

player = 'x'

while continue<sub>game</sub>(board):

print<sub>board</sub>(board)

move = ask<sub>mov</sub>(player)

if make<sub>mov</sub>(move, board, player) != 0:
    continue

player = change<sub>player</sub>(player)

    print("\nTablero Final")
    print<sub>board</sub>(board)
\#+end<sub>src</sub>>

