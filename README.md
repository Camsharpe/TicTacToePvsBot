<p align="center">
Tic Tac Toe. User vs Bot version.

 

<h2>Description</h2>
This project consist of a classic Tic Tac Toe game. I created this game in C# while taking Programming I @ KSU. Enjoy!
<br />


<h2>Languages and Utilities Used</h2>

- <b>C#</b> 
- <b>Microsoft Visual Studios</b>

<h2> C# code </h2>



          class Program
    {
        static char[] board = { ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ' };
        static char playerSymbol, botSymbol;
        static string playerName;
        

        static void Main(string[] args)
        {
            Console.WriteLine("Hello, my name is Cameron. Welcome to my Tic Tac Toe game!");
            Console.Write("Please enter your name: ");
            playerName = Console.ReadLine();
            Console.WriteLine("Nice to meet you, " + playerName + "! Enjoy the game.");
            Console.WriteLine();

            bool isPlayerTurn = true;
            bool gameOver = false;

            // Randomly assign symbols to player and bot
            Random random = new Random();
            int randomNum = random.Next(0, 2);
            playerSymbol = randomNum == 0 ? 'X' : 'O';
            botSymbol = playerSymbol == 'X' ? 'O' : 'X';

            while (!gameOver)
            {
                DrawBoard();
                if (isPlayerTurn)
                {
                    PlayerMove();
                    if (CheckWin(playerSymbol))
                    {
                        DrawBoard();
                        Console.WriteLine("Congratulations, " + playerName + "! You won!");
                        gameOver = true;
                    }
                    else if (IsBoardFull())
                    {
                        DrawBoard();
                        Console.WriteLine("It's a draw!");
                        gameOver = true;
                    }
                    isPlayerTurn = false;
                }
                else
                {
                    BotMove();
                    if (CheckWin(botSymbol))
                    {
                        DrawBoard();
                        Console.WriteLine("You lost! Better luck next time.");
                        gameOver = true;
                    }
                    else if (IsBoardFull())
                    {
                        DrawBoard();
                        Console.WriteLine("It's a draw!");
                        gameOver = true;
                    }
                    isPlayerTurn = true;
                }
            }

            Console.WriteLine("Thank you for playing Tic Tac Toe!");
            Console.ReadLine();
        }

        static void DrawBoard()
        {
            Console.Clear();
            Console.WriteLine(" " + board[0] + " | " + board[1] + " | " + board[2] + " ");
            Console.WriteLine("---+---+---");
            Console.WriteLine(" " + board[3] + " | " + board[4] + " | " + board[5] + " ");
            Console.WriteLine("---+---+---");
            Console.WriteLine(" " + board[6] + " | " + board[7] + " | " + board[8] + " ");
            Console.WriteLine();
        }

        static void PlayerMove()
        {
            bool validMove = false;
            int move;

            do
            {
                Console.Write("Enter your move (1-9): ");
                string input = Console.ReadLine();

                if (int.TryParse(input, out move))
                {
                    if (move >= 1 && move <= 9 && board[move - 1] == ' ')
                    {
                        validMove = true;
                    }
                }

                if (!validMove)
                {
                    Console.WriteLine("Invalid move! Please try again.");
                }

            } while (!validMove);

            board[move - 1] = playerSymbol;
        }

        static void BotMove()
        {
            int move;
            bool validMove = false;
            Random random = new Random();

            do
            {
                move = random.Next(1, 10);
                if (board[move - 1] == ' ')
                {
                    validMove = true;
                }
            } while (!validMove);

            board[move - 1] = botSymbol;
            Console.WriteLine("The bot has placed its symbol at position " + move);
            Console.WriteLine();
        }

        static bool CheckWin(char symbol)
        {
            if ((board[0] == symbol && board[1] == symbol && board[2] == symbol) ||
                (board[3] == symbol && board[4] == symbol && board[5] == symbol) ||
                (board[6] == symbol && board[7] == symbol && board[8] == symbol) ||
                (board[0] == symbol && board[3] == symbol && board[6] == symbol) ||
                (board[1] == symbol && board[4] == symbol && board[7] == symbol) ||
                (board[2] == symbol && board[5] == symbol && board[8] == symbol) ||
                (board[0] == symbol && board[4] == symbol && board[8] == symbol) ||
                (board[2] == symbol && board[4] == symbol && board[6] == symbol))
            {
                return true;
            }
            return false;
        }

        static bool IsBoardFull()
        {
            foreach (char c in board)
            {
                if (c == ' ')
                {
                    return false;
                }
            }
            return true;
        }
    }









<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
