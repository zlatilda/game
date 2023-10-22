# 2048 game

Description:
Implementation of 2048 game application.
Application does the following:
- Shows main menu and controls to start a game
- Implements game logic
- Enables to undo the step
- Calculates and displays user score
- Non-blocking UI
- Compiles for Linux and Windows.

 The application is made using Qt for UI and standard C/C++ libraries.


GAME CLASS

Private member variables:
- int board[4][4]: 4X4 matrix that represents game board.
- int** prev_board: saves the previous to current state of the board.
- int score: a variable that stores game score.

Public Methods
- void new_game(): This method initializes a new game by resetting the game board, setting the score to 0, and adding the first piece to the board. It should be called at the beginning of each new game.
- void apply_move(int direction: This method is used to apply a move to the game board. The direction parameter should be one of the following values:
 0 (Up), 1 (Right), 2 (Down), 3 (Left). It updates the game board based on the chosen direction, combining tiles and increasing the score as appropriate.
- int get_board_value(int i, int j): This method returns the value at the specified position (i, j) on the game board. The i parameter represents the row, and the j parameter represents the column. The board values can be 0 (empty) or powers of 2 (2, 4, 8, etc.).
- int get_score(): This method returns the current score of the game.
- void restore_to_prev_move(): This method restores the game board to its state before the last move. It is used to undo the previous action in case the player wishes to revert their move.

Private Helper Methods
- pair<int,int> generate_unoccupied_position(): This method generates an unoccupied position (empty cell) on the game board and returns it as a pair of (line, column) coordinates.
- void add_piece(): This method adds a new piece with the value of 2 to a randomly selected unoccupied position on the game board.
- bool can_do_move(int line, int column, int next_line, int next_column): This method checks whether a move is possible from a given position (line, column) to the next position (next_line, next_column) based on the current board state.
- void save_prev_move(): This method saves the current state of the game board into the prev_board array. It is used for reverting moves.

Destructor
- ~game():  The destructor is responsible for releasing the memory allocated for the prev_board array to prevent memory leaks.


MAIN WINDOW CLASS

The MainWindow class represents the primary user interface for a game application, specifically designed for the game 2048. This class is part of a graphical user interface (GUI) developed using the Qt framework and is responsible for rendering the game board, handling user input, and managing game state. MainWindow is a subclass of QMainWindow, which is a part of the Qt framework for building graphical applications.

Private Attributes
- Ui::MainWindow *ui: A pointer to the user interface object associated with the main window.
- game obj: An instance of the game class, which is responsible for managing the game's logic and data.

Public Methods
- MainWindow(QWidget *parent = nullptr): Constructor that initializes an instance of the MainWindow class. It accepts an optional QWidget parent pointer. It also initializes the random number generator and sets up the user interface.
- ~MainWindow(): Destructor that's responsible for releasing resources and cleaning up the MainWindow instance.
- void Print_matrix(): Displays the current state of the game board on the user interface, updating the colors and labels of the cells based on the game's current state.
- void Clear_screen(): Clears the game board on the user interface by resetting cell colors and labels to their default values.
- void Form_matrix(): Initializes the game board's graphical representation on the user interface by mapping labels and frames to the 4x4 grid cells.

Private Slots
- void on_pushButton_new_game_clicked(): Event handler for the "New Game" button click. It clears the screen, initializes a new game state, and updates the user interface to reflect the new game state.
- void keyPressEvent(QKeyEvent *event) override : Event handler for keyboard key presses. It interprets key presses such as "W," "A," "S," "D," and "Z" for game controls. "W," "A," "S," and "D" are used for moving the tiles in the game, and "Z" is used to undo the previous move.
- void on_actionQuit_triggered(): Event handler for the "Quit" action. This action allows the user to exit the application gracefully.
- void showEvent(QShowEvent* event) override : Event handler for the "showEvent" triggered when the main window is first displayed. It initializes a new game state and prepares the user interface for gameplay.
