python
from __future__ import print_function

board = [' ' for _ in range(9)]
player = "X"


def display_board(board):
    print("-------------")
    print("| " + board[0] + " | " + board[1] + " | " + board[2] + " |")
    print("-------------")
    print("| " + board[3] + " | " + board[4] + " | " + board[5] + " |")
    print("-------------")
    print("| " + board[6] + " | " + board[7] + " | " + board[8] + " |")
    print("-------------")


def play_game():
    display_board(board)
    while not game_over():
        turn(player)
        switch_player()
    winner = check_winner()
    if winner == "draw":
        print("Game Over. It's a draw.")
    else:
        print("Congratulations " + winner + "! You won!")


def game_over():
    return check_winner() or board.count(' ') == 0


def turn(player):
    print(player + "'s turn.")
    position = input("Choose a position from 1-9: ")
    while position not in ['1', '2', '3', '4', '5', '6', '7', '8', '9']:
        position = input("Invalid input. Choose a position from 1-9: ")
    position = int(position) - 1
    if board[position] == ' ':
        board[position] = player
        display_board(board)
    else:
        print("That position is taken. Try again.")
        turn(player)


def switch_player():
    global player
    if player == "X":
        player = "O"
    else:
        player = "X"


def check_winner():
    winner = None
    # check rows
    for row in range(0, 9, 3):
        if board[row] == board[row + 1] == board[row + 2] != ' ':
            winner = board[row]
    # check columns
    for col in range(3):
        if board[col] == board[col + 3] == board[col + 6] != ' ':
            winner = board[col]
    # check diagonal
    if board[0] == board[4] == board[8] != ' ':
        winner = board[0]
    if board[2] == board[4] == board[6] != ' ':
        winner = board[2]
    if not winner and board.count(' ') == 0:
        return "draw"
    else:
        return winner


play_game()
