# Function to print the board
def print_board(board):
    print("-------------")
    for row in board:
        print("|", " | ".join(row), "|")
    print("-------------")

# Function to check if a player has won
def check_winner(board, player):
    # Check rows, columns, and diagonals
    for i in range(3):
        if all([board[i][j] == player for j in range(3)]) or all([board[j][i] == player for j in range(3)]):
            return True
    if board[0][0] == player and board[1][1] == player and board[2][2] == player:
        return True
    if board[0][2] == player and board[1][1] == player and board[2][0] == player:
        return True
    return False

# Function to check if the board is full (draw condition)
def board_full(board):
    for row in board:
        if " " in row:
            return False
    return True

# Main function to play the game
def play_game():
    board = [[" " for _ in range(3)] for _ in range(3)]  # Initial empty board
    players = ["X", "O"]  # Two players
    turn = 0  # Track turns
    
    print("Welcome to Tic Tac Toe!")
    
    # Game loop
    while True:
        print_board(board)
        player = players[turn % 2]
        print(f"Player {player}'s turn!")
        
        # Get valid move input
        while True:
            try:
                row = int(input("Enter the row (0, 1, or 2): "))
                col = int(input("Enter the column (0, 1, or 2): "))
                if board[row][col] == " ":
                    board[row][col] = player
                    break
                else:
                    print("Cell is already occupied, try again.")
            except (ValueError, IndexError):
                print("Invalid input. Please enter row and column as numbers between 0 and 2.")
        
        # Check if the current player has won
        if check_winner(board, player):
            print_board(board)
            print(f"Player {player} wins!")
            break
        
        # Check for a draw
        if board_full(board):
            print_board(board)
            print("It's a draw!")
            break
        
        # Switch to the next player's turn
        turn += 1

# Start the game
if __name__ == "__main__":
    play_game()

