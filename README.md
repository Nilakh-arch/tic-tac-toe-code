include <stdio.h>

void newboard();
void printboard();
int availablespace();
void moveFORplayer1();
void moveFORplayer2();
char checkwinners();

const char player1 = 'X';
const char player2 = 'O';
char board[3][3];

int main() {
    newboard();
    printboard();

    while (availablespace() > 0) {
        moveFORplayer1();
        printboard();
        if (checkwinners() == player1) {
            printf("PLAYER 1 WON\n");
            return 0;
        }

        if (availablespace() == 0) {
            break;  
        }

        moveFORplayer2();
        printboard();
        if (checkwinners() == player2) {
            printf("PLAYER 2 WON\n");
            return 0;  
        }
    }

    printf("It's a draw!\n");
    return 0;
}

void newboard() {
    for (int i = 0; i < 3; i++) {           
        for (int j = 0; j < 3; j++) {
            board[i][j] = ' ';
        }
    }
}

void printboard() {
    for (int i = 0; i < 3; i++) {
        printf(" %c | %c | %c \n", board[i][0], board[i][1], board[i][2]);
        if (i < 2) {
            printf("---|---|---\n");
        }
    }
}

void moveFORplayer1() {
    int row, column;
    while (1) {
        printf("PLAYER 1, enter the row (1-3) and column (1-3): ");
        scanf("%d %d", &row, &column);
        if (row < 1 || row > 3 || column < 1 || column > 3 || board[row - 1][column - 1] != ' ') {
            printf("Invalid move, try again.\n");
        } else {
            board[row - 1][column - 1] = player1;
            break;
        }
    }
}

void moveFORplayer2() {
    int row, column;
    while (1) {
        printf("PLAYER 2, enter the row (1-3) and column (1-3): ");
        scanf("%d %d", &row, &column);
        if (row < 1 || row > 3 || column < 1 || column > 3 || board[row - 1][column - 1] != ' ') {
            printf("Invalid move, try again.\n");
        } else {
            board[row - 1][column - 1] = player2; 
            break;
        }
    }
}

int availablespace() {
    int freespace = 0;
    for (int i = 0; i < 3; i++) {           
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                freespace++;
            }
        }
    }
    return freespace; 
}

char checkwinners() {
    // Check rows
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ') {
            return board[i][0]; 
        }
    }
    
    // Check columns
    for (int j = 0; j < 3; j++) {
        if (board[0][j] == board[1][j] && board[1][j] == board[2][j] && board[0][j] != ' ') {
            return board[0][j];  
        }
    }
    
    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ') {
        return board[0][0];  
    }
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ') {
        return board[0][2]; 
    }

    return ' ';  
}
