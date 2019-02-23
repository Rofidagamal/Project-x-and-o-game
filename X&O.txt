package project_x.o;

import java.util.Scanner;

public class Project_xO {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[][] matrix;
        matrix = new String[3][3];//the matrix of the play
        int place = 1;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                matrix[i][j] = "[" + place + "]";
                place++;
            }
        }
        print_free(matrix);//print the usual shape of x o and when it is free
        int x = 0, p = 0;
        String s = new String("");
        do {
//loop to make alot of chooses to win any one or to draw
            menu();
            System.out.print("Please enter a choose :");
            x = sc.nextInt();
//function truee it makes if it input  datatype wrong or intger out the limit of matrix  input another number 
            switch (x) {
                case 1:
                    int choice,
                     row,
                     colum;
                    System.out.print("Please enter the place:");
                    choice = truee();
                    row = given_row(choice);
                    colum = given_colum(choice);
                    if (Valid_place(matrix, row, colum) == false) {
                        while (Valid_place(matrix, row, colum) == false) {
                            System.out.println("Please enter correct place,this is not avalible place:");
                            choice = truee();
                            row = given_row(choice);
                            colum = given_colum(choice);
                        }
                    }

                    p++;//counter that makes join x or o if odd x if even o
                    if (p % 2 != 0) {
                        System.out.print("Please enter the cahracter x:");
                        s = sc.next();
                        while (!s.equals("x")) {
                            System.out.print("Please enter the cahracter x:");
                            s = sc.next();

                        }
                    } else {
                        System.out.print("Please enter the cahracter o:");
                        s = sc.next();
                        while (!s.equals("o")) {
                            System.out.print("Please enter the cahracter o:");
                            s = sc.next();

                        }
                    }

                    matrix[row][colum] = "[" + s + "]";
                    //enter the char if it free
                    print_free(matrix);//the print after join any char

                    if (!WIN(matrix).equals("false")) {//if x win or o win break and the program finish
                        System.out.println(WIN(matrix));
                        break;
                    }
                    break;
                case 2:
                    int choice2,
                     row2,
                     colum2;
                    System.out.print("Please enter a place you want to cancel:");
                    choice2 = truee();
                    row2 = given_row(choice2);
                    colum2 = given_colum(choice2);
                    if (matrix[row2][colum2].equals("[" + choice2 + "]")) {
                        System.out.println("That is already free");//if the place was free before!
                    } else {
                        matrix[row2][colum2] = "[" + choice2 + "]";
                        --p;
                    }//that is make counter to enter the char has canceled again
                    print_free(matrix); //print the shape after cancel
                    break;
                default:
                    System.out.print("Enter correct choose:");//if it is enter choose not 1 or 2 enter another
                    break;
            }
            if (!WIN(matrix).equals("false"))//if any player win break
            {
                break;
            } else if (WIN(matrix).equals("false") && p == 9)//if it is no free places and no one win that mean draw
            {
                System.out.println("Draw");
                break;
            }
        } while (WIN(matrix).equals("false") || fun2(matrix).equals("true"));
    }/*this loop to enter chooses to continue if no one win
     and if there were places free*/


    public static String fun2(String[][] matrix) {//fun return true if there were places free and false if it all not free
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (matrix[i][j].equals("[ ]")) {
                    return "true";
                }
            }
        }
        return "false";
    }

    public static void menu()//this is menu to show the opinions
    {
        System.out.println("Please press 1 if you want to input ");
        System.out.println("Please press 2 if you want to cancel");
        System.out.println("~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");

    }

    public static void print_free(String[][] matrix) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }

    public static int truee() {
        Scanner input = new Scanner(System.in);
        while (input.hasNext()) {
            if (input.hasNextInt()) {
                int x = input.nextInt();
                if (x >= 1 && x <= 9) {
                    return x;
                }

            } else {
                System.out.println("Please enter a correct intger in range [1,3]");
            }
            input.next();
        }
        return 0;
    }

    public static String WIN(String[][] matrix) {//if any player win 
        String win = "";
        if (matrix[0][0].equals(matrix[0][1]) && matrix[0][1].equals(matrix[0][2])
                && !matrix[0][0].equals("[ ]")) {
            if (matrix[0][0].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[1][0].equals(matrix[1][1]) && matrix[1][1].equals(matrix[1][2])
                && !matrix[1][1].equals("[ ]")) {
            if (matrix[1][1].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[2][0].equals(matrix[2][1]) && matrix[2][1].equals(matrix[2][2])
                && !matrix[2][2].equals("[ ]")) {
            if (matrix[2][2].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[0][0].equals(matrix[1][0]) && matrix[1][0].equals(matrix[2][0])
                && !matrix[0][0].equals("[ ]")) {
            if (matrix[0][0].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[0][1].equals(matrix[1][1]) && matrix[1][1].equals(matrix[2][1])
                && !matrix[1][1].equals("[ ]")) {
            if (matrix[1][1].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[0][2].equals(matrix[1][2]) && matrix[1][2].equals(matrix[2][2])
                && !matrix[2][2].equals("[ ]")) {
            if (matrix[2][2].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[0][0].equals(matrix[1][1]) && matrix[1][1].equals(matrix[2][2])
                && !matrix[2][2].equals("[ ]")) {
            if (matrix[2][2].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else if (matrix[0][2].equals(matrix[1][1]) && matrix[1][1].equals(matrix[2][0])
                && !matrix[1][1].equals("[ ]")) {
            if (matrix[1][1].equals("[x]")) {
                win = "Player X is win";
            } else {
                win = "Player O is win";
            }
        } else {
            win = "false";
        }
        return win;

    }

    public static boolean Valid_place(String[][] matrix, int row, int colum) {//check that is valid place
        if (matrix[row][colum].equals("[1]")) {
            return true;
        } else if (matrix[row][colum].equals("[2]")) {
            return true;
        } else if (matrix[row][colum].equals("[3]")) {
            return true;
        } else if (matrix[row][colum].equals("[4]")) {
            return true;
        } else if (matrix[row][colum].equals("[5]")) {
            return true;
        } else if (matrix[row][colum].equals("[6]")) {
            return true;
        } else if (matrix[row][colum].equals("[7]")) {
            return true;
        } else if (matrix[row][colum].equals("[8]")) {
            return true;
        } else if (matrix[row][colum].equals("[9]")) {
            return true;
        } else {
            return false;
        }
    }

    public static int given_row(int x) {//take the place return the row of the place
        if (x == 1 || x == 2 || x == 3) {
            return 0;
        } else if (x == 4 || x == 5 || x == 6) {
            return 1;
        } else {
            return 2;
        }
    }

    public static int given_colum(int x) {//take the place return the colum of the place
        if (x == 1 || x == 4 || x == 7) {
            return 0;
        } else if (x == 2 || x == 5 || x == 8) {
            return 1;
        } else {
            return 2;
        }
    }

}
