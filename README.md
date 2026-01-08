#include <stdio.h>

char board[3][3];
char currentPlayer;

/* Function declarations */
void initializeBoard();
void displayBoard();
void switchPlayer();
char checkWinner();

/* Main function */
int main() {
    int row, col;
    char winner = ' ';

    initializeBoard();
    currentPlayer = 'X';

    while (winner == ' ') {
        displayBoard();

        printf("Player %c, enter row (1-3) and column (1-3): ", currentPlayer);
        scanf("%d %d", &row, &col);

        row--; 
        col--;

        if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            printf("Invalid move! Try again.\n");
            continue;
        }

        board[row][col] = currentPlayer;
        winner = checkWinner();

        if (winner == ' ')
            switchPlayer();
    }

    displayBoard();

    if (winner == 'D')
        printf("The game is a draw!\n");
    else
        printf("Player %c wins!\n", winner);

    return 0;
}

/* Initialize board */
void initializeBoard() {
    int i, j;
    for (i = 0; i < 3; i++)
        for (j = 0; j < 3; j++)
            board[i][j] = ' ';
}

/* Display board */
void displayBoard() {
    int i;
    printf("\n");
    for (i = 0; i < 3; i++) {
        printf(" %c | %c | %c \n", board[i][0], board[i][1], board[i][2]);
        if (i < 2)
            printf("---|---|---\n");
    }
    printf("\n");
}

/* Switch player */
void switchPlayer() {
    if (currentPlayer == 'X')
        currentPlayer = 'O';
    else
        currentPlayer = 'X';
}

/* Check winner */
char checkWinner() {
    int i;

    for (i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] &&
            board[i][1] == board[i][2] &&
            board[i][0] != ' ')
            return board[i][0];

        if (board[0][i] == board[1][i] &&
            board[1][i] == board[2][i] &&
            board[0][i] != ' ')
            return board[0][i];
    }

    if (board[0][0] == board[1][1] &&
        board[1][1] == board[2][2] &&
        board[0][0] != ' ')
        return board[0][0];

    if (board[0][2] == board[1][1] &&
        board[1][1] == board[2][0] &&
        board[0][2] != ' ')
        return board[0][2];

    for (i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            if (board[i][j] == ' ')
                return ' ';

    return 'D';  // Draw
}
