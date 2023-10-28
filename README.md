import java.util.Random;
import java.util.Scanner;
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

public class TicTacToe {

    static ArrayList<Integer> playerpositions = new ArrayList<Integer>();
    static ArrayList<Integer> cpupositions = new ArrayList<Integer>();

    public static void main(String[] args) {
        char[][] gameBoard = { { ' ', '|', ' ', '|', ' ' },
                { '-', '+', '-', '+', '-' },
                { ' ', '|', ' ', '|', ' ' },
                { '-', '+', '-', '+', '-' },
                { ' ', '|', ' ', '|', ' ' } };

        printGameBoard(gameBoard);

        while (true) {
            Scanner scan = new Scanner(System.in);
            System.out.println("Enter your placement (1-9)");
            int playerPos = scan.nextInt();
            while (playerpositions.contains(playerPos) || cpupositions.contains(playerPos)) {
                System.out.println("Position taken! Enter a correct Position");
                playerPos = scan.nextInt();
            }
            
            placePiece(gameBoard, playerPos, "player");
            printGameBoard(gameBoard);

            String result = checkWinner();
            if (!result.equals(" ")) {
                System.out.println(result);
                break;
            }

            Random rand = new Random();
            int cpuPos = rand.nextInt(9) + 1;
            while (playerpositions.contains(cpuPos) || cpupositions.contains(cpuPos)) {
                cpuPos = rand.nextInt(9) + 1;
            }
            
            placePiece(gameBoard, cpuPos, "cpu");
            printGameBoard(gameBoard);

            result = checkWinner();
            if (!result.equals(" ")) {
                System.out.println(result);
                break;
            }
        }
    }

    public static void printGameBoard(char[][] gameBoard) {
        for (char[] row : gameBoard) {
            for (char c : row) {
                System.out.print(c);
            }
            System.out.println();
        }
    }

    public static void placePiece(char[][] gameBoard, int pos, String user) {
        char symbol = ' ';
        if (user.equals("player")) {
            symbol = 'X';
            playerpositions.add(pos);
        } else if (user.equals("cpu")) {
            symbol = 'O';
            cpupositions.add(pos);
        }
        switch (pos) {
            case 1:
                gameBoard[0][0] = symbol;
                break;
            case 2:
                gameBoard[0][2] = symbol;
                break;
            case 3:
                gameBoard[0][4] = symbol;
                break;
            case 4:
                gameBoard[2][0] = symbol;
                break;
            case 5:
                gameBoard[2][2] = symbol;
                break;
            case 6:
                gameBoard[2][4] = symbol;
                break;
            case 7:
                gameBoard[4][0] = symbol;
                break;
            case 8:
                gameBoard[4][2] = symbol;
                break;
            case 9:
                gameBoard[4][4] = symbol;
                break;
            default:
                break;
        }
    }

    public static String checkWinner() {
        List<Integer> topRow = Arrays.asList(1, 2, 3);
        List<Integer> middleRow = Arrays.asList(4, 5, 6);
        List<Integer> botRow = Arrays.asList(7, 8, 9);
        List<Integer> leftCol = Arrays.asList(1, 4, 7);
        List<Integer> midCol = Arrays.asList(2, 5, 8);
        List<Integer> rightCol = Arrays.asList(3, 6, 9);
        List<Integer> diag1 = Arrays.asList(1, 5, 9);
        List<Integer> diag2 = Arrays.asList(7, 5, 3);

        List<List<Integer>> winning = new ArrayList<List<Integer>>();
        winning.add(topRow);
        winning.add(middleRow);
        winning.add(botRow);
        winning.add(leftCol);
        winning.add(midCol);
        winning.add(rightCol);
        winning.add(diag1);
        winning.add(diag2);

        for (List<Integer> l : winning) {
            if (playerpositions.containsAll(l)) {
                return "Congratulations, you won!";
            } else if (cpupositions.containsAll(l)) {
                return "CPU has won. Sorry :(";
            } else if (playerpositions.size() + cpupositions.size() == 9) {
                return "CAT";
            }
        }

        return " ";
    }
}
