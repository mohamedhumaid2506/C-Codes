#include <stdio.h>

char board[3][3];

void initializeBoard() {
    int num = 1;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = num++ + '0';
        }
    }
}

void displayBoard() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf("  %c  ", board[i][j]);
            if (j < 2) {
                printf("|");
            }
        }
        printf("\n");
        if (i < 2) {
            for (int j = 0; j < 3; j++) {
                printf("____ ");
                if (j < 2) {
                    printf("|");
                }
            }
            printf("\n");
        }
    }
}

int checkWin() {
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2])
            return 1;
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i])
            return 1;
    }
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2])
        return 1;
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0])
        return 1;

    return 0;
}

int isDraw() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] >= '1' && board[i][j] <= '9') {
                return 0;
            }
        }
    }
    return 1;
}

void makeMove(char player) {
    int choice;
    int validMove = 0;

    while (!validMove) {
        printf("Player %c, enter your move (1-9): ", player);
        scanf("%d", &choice);

        if (choice >= 1 && choice <= 9) {
            int row = (choice - 1) / 3;
            int col = (choice - 1) % 3;

            if (board[row][col] >= '1' && board[row][col] <= '9') {
                board[row][col] = player;
                validMove = 1;
            } else {
                printf("Invalid move! Position already taken.\n");
            }
        } else {
            printf("Invalid input! Enter a number between 1 and 9.\n");
        }
    }
}

int main() {
    char player = 'X';
    initializeBoard();

    while (1) {
        displayBoard();

        makeMove(player);

        if (checkWin()) {
            displayBoard();
            printf("Player %c wins!\n", player);
            break;
        }

        if (isDraw()) {
            displayBoard();
            printf("It's a draw!\n");
            break;
        }

        player = (player == 'X') ? 'O' : 'X';
    }

    return 0;
}
