# Игра "Крестики-Нолики"

def print_board(board):
    """Выводит игровое поле"""
    for i in range(3):
        print(" | ".join(board[i]))
        if i < 2:
            print("---------")

def check_win(board):
    """Проверяет наличие победной комбинации"""
    # Проверка строк и столбцов
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != ' ': return True
        if board[0][i] == board[1][i] == board[2][i] != ' ': return True

    # Проверка диагоналей
    if board[0][0] == board[1][1] == board[2][2] != ' ': return True
    if board[0][2] == board[1][1] == board[2][0] != ' ': return True

    return False

def is_draw(board):
    """Проверяет, закончилась ли игра вничью (все клетки заполнены)"""
    for row in board:
        if ' ' in row:
            return False
    return True

def make_move(player, board):
    """Позволяет игроку сделать ход"""
    while True:
        try:
            x = int(input(f"Введите номер строки для {player}: "))
            y = int(input(f"Введите номер столбца для {player}: "))
            if 1 <= x <= 3 and 1 <= y <= 3 and board[x-1][y-1] == ' ':
                board[x-1][y-1] = player
                break
            else:
                print("Неверные координаты. Попробуйте снова.")
        except ValueError:
            print("Пожалуйста, введите числа от 1 до 3.")

if __name__ == "__main__":
    # Инициализация игрового поля
    board = [[' '] * 3 for _ in range(3)]
    
    current_player = 'X'
    game_over = False

    while not game_over:
        print_board(board)
        
        make_move(current_player, board)
        
        if check_win(board):
            print(f"Победил игрок {current_player}!")
            game_over = True
        elif is_draw(board):
            print("Ничья!")
            game_over = True
        else:
            current_player = 'O' if current_player == 'X' else 'X'

    print_board(board)
 
