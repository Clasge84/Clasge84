import numpy as np

def initialize_game():
    return np.full((3, 3), ' ')

def display_board(board):
    print(board)

def check_win(board):
    for row in board:
        if all(symbol == 'X' for symbol in row) or all(symbol == 'O' for symbol in row):
            return True
    for col in board.T:
        if all(symbol == 'X' for symbol in col) or all(symbol == 'O' for symbol in col):
            return True
    if all(board[i, i] == 'X' for i in range(3)) or all(board[i, i] == 'O' for i in range(3)):
        return True
    if all(board[i, 2-i] == 'X' for i in range(3)) or all(board[i, 2-i] == 'O' for i in range(3)):
        return True
    return False

def check_draw(board):
    return ' ' not in board

def handle_move(board, player):
    while True:
        try:
            row = int(input(f"Player {player}, enter row (0-2): "))
            col = int(input(f"Player {player}, enter column (0-2): "))
            if board[row, col] == ' ':
                board[row, col] = player
                break
            else:
                print("Position already taken. Try again.")
        except ValueError:
            print("Invalid input. Please enter a number.")
        except IndexError:
            print("Invalid input. Row and column must be in range 0-2.")

def switch_player(player):
    return 'O' if player == 'X' else 'X'

def main():
    while True:
        board = initialize_game()
        player = 'X'
        while True:
            display_board(board)
            handle_move(board, player)
            if check_win(board):
                display_board(board)
                print(f"Player {player} wins!")
                break
            elif check_draw(board):
                display_board(board)
                print("It's a draw!")
                break
            player = switch_player(player)
        play_again = input("Do you want to play again? (yes/no): ")
        if play_again.lower() != 'yes':
            break

if __name__ == "__main__":
    main()
