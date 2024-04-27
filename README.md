class ChessGame:
    def __init__(self):
        self.board = self.create_board()
        self.current_player = 'white'
        self.game_over = False

    def create_board(self):
        board = []
        for _ in range(8):
            row = [' '] * 8
            board.append(row)
        # Place pieces
        board[0] = ['r', 'n', 'b', 'q', 'k', 'b', 'n', 'r']
        board[1] = ['p'] * 8
        board[6] = ['P'] * 8
        board[7] = ['R', 'N', 'B', 'Q', 'K', 'B', 'N', 'R']
        return board

    def print_board(self):
        for row in self.board:
            print(' '.join(row))

    def move_piece(self, start, end):
        start_row, start_col = start
        end_row, end_col = end
        piece = self.board[start_row][start_col]
        if piece == ' ':
            print("No piece there!")
            return False
        if self.current_player == 'white' and piece.islower():
            print("It's black's turn!")
            return False
        if self.current_player == 'black' and piece.isupper():
            print("It's white's turn!")
            return False
        # Check if move is valid, implement rules here
        self.board[end_row][end_col] = piece
        self.board[start_row][start_col] = ' '
        return True

    def switch_turn(self):
        self.current_player = 'black' if self.current_player == 'white' else 'white'

    def play(self):
        while not self.game_over:
            self.print_board()
            print(f"{self.current_player}'s turn.")
            start = tuple(map(int, input("Enter start position (row, col): ").split(',')))
            end = tuple(map(int, input("Enter end position (row, col): ").split(',')))
            if self.move_piece(start, end):
                self.switch_turn()

game = ChessGame()
game.play()
