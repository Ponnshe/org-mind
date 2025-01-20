
# Table of Contents

1.  [Objective](#org8f7dcdc)
2.  [Fleeting](#org5f57de1)
    1.  [Python](#org9d968d7)
        1.  [Planning](#org7d21412)
        2.  [Implementation](#org9c26d78)
3.  [See Also](#org96f4bcd)



<a id="org8f7dcdc"></a>

# Objective

Write a function named `isValidChessBoard()` that receive that takes a dictionary argument and returns True
or False depending on if the board is valid.
A valid board will have exactly one black king and exactly one white king. Each player can only have at most 16 pieces, at most 8 pawns, and all pieces must be on a valid space from '1a' to '8h'; that is, a piece can’t be on space '9z'. The piece names begin with either a 'w' or 'b' to represent white or black, followed by 'pawn', 'knight', 'bishop', 'rook', 'queen', or 'king'. This function should detect when a bug has resulted in an improper chess
board.


<a id="org5f57de1"></a>

# Fleeting

This will chaotic because I will just write and annotate my thoughts as they come, later (if I want) I will write a cleaner version.

Another thing to consider is that I love the early return approach so I will use it. Briefly, the early return approach let me use many returns within a function to exit the function earlier, instead of using just one return statement at the end. The early return approach avoid deep nested control statements


<a id="org9d968d7"></a>

## Python

This is an example of a dictionary that I will receive in the function

    chess_board = {
        '1h': 'bking',
        '6c': 'wqueen',
        '2g': 'bbishop',
        '5h': 'bqueen',
        '3e': 'wking'
    } 


<a id="org7d21412"></a>

### Planning

The chess board has some requierements to meet in order to be consider a valid chess board, therefore I will have to check for those requirements:

-   Check if there is just one black king and one white king, **Check for kings**
-   At most 16 pieces for player
-   At most 8 pawns for player
-   Positions must be between `1a` and `8h`
-   Piece name must start with `b` or `w`
-   The valid pieces are {"pawn", "knight", "bishop", "rook", "queen","king"}

Now I will order these requirements in a way in which the fastest ones to check and the most excluyents are at the top and the most laborious ones and less excluyents are at the bottom:

-   [X] **Name in standard way**: Piece name must start with `b` or `w`
-   [X] **Valid Position**: Positions must be between `1a` and `8h`
-   [X] **Valid Piece**: The valid pieces are {"pawn", "knight", "bishop", "rook", "queen","king"}
-   [X] **Valid Number of kings** Check if there is just one black king and one white king.
-   [X] **Valid Number of pawns**:  At most 8 pawns for player
-   [X] **Valid number of pieces for player**: At most 16 pieces for player

I choose this order because the first three just need one case to declare the table invalid, while the last three require to consider at least two cases to mark the table as invalid. I mean:
`Name in standard way`, `Valid Position` and `Valid Piece` with just one case that is wrong they can declare the table as invalid. `Valida Number of Kings` needs to observe two kings of the same color to mark the table as invalid, `Valid number of pawns` require to observe 9 pawns of the same color to declare the table as invalid, and `Valid number of pieces for player` needs 17 pieces of the same color to say that the table is wrong. So you can see how the number of require cases to see increments along the list.

Another thing to consider in the selected order of the requirements is that all of them are operations that can be done in lineal time in the worst case scenario. So its computational complexity is of $ O(n)\ ). This is because in the worst case we need to check all the dictionary entries, the first three requirements needs to grab the names and positions and checks them against a list of valid values, but the lenghts of these lists are constants, so every one of them has a computational complexity of \( O(n*k) $ where k is constant so it is $ O(n) $ and the last three are just $ O(n) $. Then, the complexity of all the function will be $ cO(n) $ where $ c $ is constant. In conclution, the function `isValidChessBoard()` must be of $ O(n) $ complexity. This reasoning leave us with just one characteristic to order the requirements and it is which can exclude a chess board the fastest

So now that I have stablish the requirements to meet I can start thinking how I will solve this. First of all **modularity** is god, so I will need to declare more functions additionally to the one asked. Hopefully there will be as much functions as the requirements, there are cases in which can be less (weird) and cases in which can be more (standard). I will use these functions:

-   `name_follows_standard()`
-   `is_valid_position()`
-   `is_valid_piece()`
    And here I realize, there's a chance that I just need this three functions because for the last three requirements I just need to count the appearance of specific cases I will need to keep auxiliar variables to count them and some if statements but no more.
    
    Now let's talk about more about the functions:

1.  name<sub>follow</sub><sub>standards</sub>(name)

    -   **name**: [str] the name of a chess piece
    
    To do this function I will just receive a `name` of a piece wich will be the value part of the dictionary. Then I will have to if check `name[0]` is `b` or `w` if not I will return false.  But I also have to check if `name` is not empty.
    
    -   [X] Check if the entry is valid
    -   [X] Check if `name[0] \== 'b'` or `name[0] == 'w'`
    
    So this can be a possible code:
    
    [Python Strings](20250114133247-python_strings.md)
    
        def name_follow_standard(name):
            if not name:
                return False
            if name[0] == 'w' or name[0] == 'b':
                return True
        
            return False
    
    We can use this approach or we can use the `try...except` block. I won't do it because this is a simple program and I am sure that I wont have and invalid entry. So this approach is more efficient and easier, but the `try...except` is more robust.

2.  is<sub>valid</sub><sub>position</sub>(position)

    -   **position**: [str] the position of a piece in a chess board
    
    For this function I will need to check a received `position` to se if it is between `1a` and `8h`. This is easy I just need to check if `position[0]` is not in [0,8] or `position[1]` is not in [a,h] if one of them is true then I will return false. <del>Mind blowing</del>
    
    -   [X] Check if the entry is valid
    -   [X] Check if `position[0] not in range(0,9)`
    -   [ ] Check if `position[1] not in range ('a', 'b')`
    
    This can be a valid code:
    
        def is_valid_position(position):
            if not position:
                return False
            if position[0] not in range(0,9):
                return False
            if positon[1] not in range ('a','i'): #I know this can't be done, but there most be a way
                return False
            return True
    
    I have to remember to check the entry. Later I will deal with the problem of creating a list from 'a' to 'h', in the worst case i will have to write manually ['a','b','c', &#x2026;, 'h']

3.  is<sub>valid</sub><sub>piece</sub>(piece)

    -   **piece**: The name of a piece
        
        Here there are two ways to approach this: I can ask for just the name of a piece without the character that tells me the color or I could just deal with it within the function. Either way I will have to write the same block of code, so let's deal with it within the function in that way I won't have to care about it in the main function.
        
        So I will need to "format" the `piece` entry to delete the first character, threfore I will have to do a slicing of the entry string and then check if the sliced part will have to be checked if it is a valid piece, I can use a list of valid pieces to check it. So:
        
        -   [X] Check the entry (**always**)
        -   [X] Slice the string
        -   [X] Check with the list
            
            A possible code could be:
    
        def is_valid_piece(piece):
            if not piece:
                return False
            piece_name=piece[1::]
            lst_pieces=["pawn", "knight", "bishop", "rook", "queen","king"]
            if piece_name in lst_pieces:
                return True
            return False

4.  isValidChessBoard(board)

    This is the main function basically I will use a for loop to iterate over the keys and values and pass them to the the previous functions. Also I will keep some variables to count the kings, pawns and pieces of every team
    
    -   [X] Check the entry
    -   [X] for loop and call the previous functions
    -   [X] Count the kings
    -   [X] Count the pawns
    -   [X] Count the pieces
        
        To "count" the kings I will just use bool variables. This variable will start as false which will represent that the program hasn't encounter any king of an specific color, when the program encounter a king of a color the corresponding variable will change to True so the next time that encounter a king of the same color and the variable is True would represent that the board is invalid.
        
        Just because is python and the program is simple this approach would not represent a difference. However, in theory, the boolean approach is more efficient because a bool variable should just require a bit to be represented, while an int variable would need 4 bytes. Again, this is just in basic theory because we should consider mem alignment.
        
        So this could be a valid code:
        
            def isValidChessBoard(board):
                if not board:
                    return False
                #Variables to "count" the kings
                there_is_bking = False;
                there_is_wking = False;
            
                #Variables to count the pawns
                bpawns_counter = 0
                wpawns_counter = 0
            
                #Variables to count the pieces
                bpieces_counter = 0
                wpieces_counter = 0
            
                for position, piece in board:
                    if not name_follow_standard(piece): #Check for name
                        return False
                    if not is_valid_position(position): #Check for position
                        return False
                    if not is_valid_piece(piece): #Check por piece
                        return False
            
                    #Check for kings
                    if piece == 'bking': #Black King
                        if there_is_bking:
                            return False
                        there_is_bking = True
            
                    if piece == 'wking': #White King
                        if there_is_wking:
                            return False
                       there_is_wking = True
            
                    #Count pawns and pieces
                    if piece[0] = 'b':
                       bpieces_counter += 1 
                       if piece[1::] = 'pawn'
                            bpawns_counter += 1
                    elif piece = 'w':
                        wpieces_counter += 1
                        if piece[1::] = 'pawn':
                            wpawns_counter += 1
            
                    #Check for number of pawns
                    if bpawns_counter > 8 or wpawns_counter > 8:
                        return False
            
                    #Check for number of pieces
                    if bpieces_counter > 16 or wpieces_counter > 16:
                        return False
                    return True
    
    One can save lines of codes by reducing some of cases to just one big case, but I don't like large lines of if cases


<a id="org9c26d78"></a>

### Implementation

Let's see how well this code performence, obviously I will have to change somethings and solve some problems. Let's remember that requeriment list

-   [X] **Name in standard way**: Piece name must start with `b` or `w`
-   [X] **Valid Position**: Positions must be between `1a` and `8h`
-   [X] **Valid Piece**: The valid pieces are {"pawn", "knight", "bishop", "rook", "queen","king"}
-   [ ] **Valid Number of kings** Check if there is just one black king and one white king.
-   [ ] **Valid Number of pawns**:  At most 8 pawns for player
-   [ ] **Valid number of pieces for player**: At most 16 pieces for player

1.  name<sub>follow</sub><sub>standards</sub>(piece)

    I will change the name of the parameter for "piece" instead of "name" just because I feel it is better.
    
        def name_follow_standard(piece):
            if not piece:
                return False
            if piece[0] == 'w' or piece[0] == 'b':
                return True
        
            return False

2.  is<sub>valid</sub><sub>position</sub>(position)

    Well for this function the way to solve the case to check the second character of the position value is valid is just check that character is in a string form by the valid characters. So:
    
        def is_valid_position(position):
            if not position:
                return False
            if position[0] not in range(0,9):
                return False
            if position[1] not in 'abcdefgh': 
                return False
            return True
    
    But this code has also an error an it is that I didn't consider the data type and the range, when I check position[0] against range(0,9) I am checking if '1' is in [0,1,2,3,4,5,6,7,8]. So to solve this problem I have to convert position[0] to int using `int(position[0])` and adjust the range to `range(1,9)`. So this is the final code:
    
        def is_valid_position(position):
            if not position:
                return False
            if int(position[0]) not in range(1,9):
                return False
            if position[1] not in 'abcdefgh': 
                return False
            return True

3.  is<sub>valid</sub><sub>piece</sub>(piece)

    I have just thought that I can use this code just because, before using this function in the siValidChess function I have check that the piece name follows the standard, so I know that piece[0] is the color character and the rest is the name of the piece
    
        def is_valid_piece(piece):
            if not piece:
                return False
            piece_name=piece[1::]
            lst_pieces=["pawn", "knight", "bishop", "rook", "queen","king"]
            if piece_name in lst_pieces:
                return True
            return False

4.  isValidChess(board)

    The first error that I notice with this function is that I forgot to use the items() method with the dictionary in the for loop to get all the keys and values.
    There is a logic error, because I forgot the there must be a king of each color to be a valid chess board because one can not play if one doesn't have a king. So this is the last code:
    
        def isValidChess(board):
            if not board:
                return False
            #Variables to "count" the kings
            there_is_bking = False;
            there_is_wking = False;
        
            #Variables to count the pawns
            bpawns_counter = 0
            wpawns_counter = 0
        
            #Variables to count the pieces
            bpieces_counter = 0
            wpieces_counter = 0
        
            for position, piece in board.items():
                if not name_follow_standard(piece): #Check for name
                    return False
                if not is_valid_position(position): #Check for position
                    return False
                if not is_valid_piece(piece): #Check for piece
                    return False
        
                #Check for kings
                if piece == 'bking': #Black King
                    if there_is_bking:
                        return False
                    there_is_bking = True
        
                if piece == 'wking': #White King
                    if there_is_wking:
                        return False
                    there_is_wking = True
        
                #Count pawns and pieces
                if piece[0] == 'b':
                   bpieces_counter += 1 
                   if piece[1::] == 'pawn':
                        bpawns_counter += 1
                elif piece == 'w':
                    wpieces_counter += 1
                    if piece[1::] == 'pawn':
                        wpawns_counter += 1
        
                #Check for number of pawns
                if bpawns_counter > 8 or wpawns_counter > 8:
                    return False
        
                #Check for number of pieces
                if bpieces_counter > 16 or wpieces_counter > 16:
                    return False
            if not there_is_bking or not there_is_wking:
                return False
            return True


<a id="org96f4bcd"></a>

# See Also

-   [Python List](20250111131854-python_list.md)
-   [Python try&#x2026;except block](20250114131635-python_try_except_block.md)
-   [Python range()](20250114135034-python_range.md)

