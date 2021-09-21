# Very-basic-Tic-tac-toe-Game
#This is my first project. It is a small and very basic 2 player tic-tac-toe game
# The project is broken down into Steps 
# Step 1
from IPython.display import clear_output


# this step creates the visual board for the players to see
def display_board(board):
    clear_output()
    print(board[1] + '|' + board[2] + '|' + board[3])
    print('-----')
    print(board[4] + '|' + board[5] + '|' + board[6])
    print('-----')
    print(board[7] + '|' + board[8] + '|' + board[9])


# step 2
def player_input():
    marker = ''
    while marker != 'X' and marker != 'O':
        marker = input('Player 1 Choose X or O').upper()

    if marker == 'X':
        return ('X', 'O')

    else:
        return ('O', 'X')
    # these are the exact things that are
    # going to show up in the boxes
    # ex. if it retuned "player x"
    # then thats exactly what would
    # appear in box
#step 3
def place_marker(board, marker, position):
    #this is to assigns marker to one of the 9 positions
    board[position] = marker
#step 4
def win_check(board,mark):
    #the purpose of this is to determine a winner
    # to see if any player gets 3 in a row
    return ((board[1] == mark and board[2] == mark and board [3] == mark)
    # at the top row
or (board[4] == mark and board[5] == mark and board[6] == mark)
    #for the middle row
or (board[7] == mark and board[8] == mark and board[9]== mark)
    #for the bottom row
or (board[7] == mark and board[5]== mark and board[3]== mark)
    #diagonal row
or (board[9]== mark and board[5]== mark and board[1]== mark)
    #for the other diagonal row
or (board[9] == mark and board[6]== mark and board [3]==mark)
    #for right vertical row
or (board[7] == mark and board[4] == mark and board[1] == mark))
    #for the left vertical row

#step 5
import random

def choose_first():
    #choosing a random player and assigning them to
    # one of the two options available
    coinFlip = random.randint(0,1)
    if coinFlip == 0:
        return 'Player 2'
    else:
        return 'Player 1'
#Step 6
def space_check(board, position):
    #to make sure empty spaces == True
    return board[position] == ' '


# Step 7
def full_board_check(board):
    # this is to check if the board is full or not
    # use for loop to determine if each block is full
    for x in range(1, 10):  # --> bc theres 9 boxes
        # if its on the board
        if space_check(board, x):
            return False

    # must be for return
    return True


# step 8
def player_choice(board):
    # must start off with 0 position
    position = 0

    # create while loop to make sure its not in
    # 1 of 9 position --> [1-->9]
    while position not in [1, 2, 3, 4, 5, 6, 7, 8, 9] or not space_check(board, position):
        # make input integer for position
        position = int(input('Choose your next position: (1 - 9)'))
    return position


#Step9
    # ask if players wanna play a game
def replay():
    return input(' Do you wanna run it again? Enter Yes or No').lower().startswith('y')


# Step 10
    # now use while loops to tun the game and
    # return commands to the players
print('Tic tac toe..... The GAME')

while True:
    # reset the board
    theBoard = [' '] * 10
    player1_marker, player2_marker = player_input()

    # randome choice
    turn = choose_first()
    print(turn + ' Will go First')

    play_game = input('Are you ready to go?? Enter Yes or No....')

    if play_game.lower()[0] == 'y':
        game_on = True
    else:
        game_on = False
    while game_on:
        if turn == 'Player 1':
            # player 1's turn

            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player1_marker, position)

            if win_check(theBoard, player1_marker):
                display_board(theBoard)
                print('Congrats YOU WON!!!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('Its a tie Game')
                    break
                else:
                    turn = 'Player 2'

        else:
            # player 2 turn

            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player2_marker, position)

            if win_check(theBoard, player2_marker):
                display_board(theBoard)
                print('Player 2 has won the game!!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('its a draw...')
                    break
                else:
                    turn = 'Player 1'
    if not replay():
        break

