import java.util.Scanner;

public class TicTacToe {

    private static final char EMPTY = '-';
    private static final char[][] initialBoard = {
        {EMPTY, EMPTY, EMPTY},
        {EMPTY, EMPTY, EMPTY},
        {EMPTY, EMPTY, EMPTY}
    };

    public static void main(String[] args) {
        char[][] board = initialBoard.clone();
        Scanner scanner = new Scanner(System.in);
        char currentPlayer = 'X';
        boolean gameFinished = false;

        printBoard(board);

        while (!gameFinished) {
            System.out.println("Player " + currentPlayer + ", make your move: ");
            int row = scanner.nextInt();
            int col = scanner.nextInt();

            if (row < 1 || row > 3 || col < 1 || col > 3) {
                System.out.println("Invalid move, try again");
                continue;
            }

            if (board[row - 1][col - 1] != EMPTY) {
                System.out.println("Invalid move, position already occupied, try again");
                continue;
            }

            board[row - 1][col - 1] = currentPlayer;
            printBoard(board);

            gameFinished = checkWinner(board, currentPlayer) || isFull(board);

            if (!gameFinished) {
                currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
            }
        }

        scanner.close();
    }

    private static void printBoard(char[][] board) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    private static boolean checkWinner(char[][] board, char player) {
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == player && board[i][1] == player && board[i][2] == player) {
                return true;
            }

            if (board[0][i] == player && board[1][i] == player && board[2][i] == player) {
                return true;
            }
        }

        if (board[0][0] == player && board[1][1] == player && board[2][2] == player) {
            return true;
        }

        if (board[0][2] == player && board[1][1] == player && board[2][0] == player) {
            return true;
        }

        return false;
    }

    private static boolean isFull(char[][] board) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == EMPTY) {
                    return false;
                }
            }
        }

        return true;
    }

    public static char getEmpty() {
        return EMPTY;
    }

    public static char[][] getInitialboard() 
    {
        return initialBoard;
    }
}
