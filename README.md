DrawTriangle
============

Console app that draws Triangle

using System;
using System.Threading;

class DrawTriangle
{
    static void Main()
    {
        Console.BufferWidth = 190;

        Console.Title = "Triangle";

        Console.WriteLine("Моля въведи символ с който ще се начертае триъгълника ");
        Console.WriteLine("за произволен символ въведи '0'");

        char drawSign = char.Parse(Console.ReadLine());

        char emptySpace = ' ';

        Console.WriteLine("Моля въведи брой символи от който ще се състой ");
        Console.WriteLine("триъгълника за произволен триъгълник въведи '0'");

        int elementCount = int.Parse(Console.ReadLine());

        Console.WriteLine("Моля въведи цвят на триъгълника -'white','red' или 'green'");
        Console.WriteLine("за произволен цвят въведи 'random'");

        string colorType = Console.ReadLine();
        
        Entrance(drawSign, emptySpace, elementCount, colorType);
    }

    private static void Entrance(char drawSign, char emptySpace, int elementCount, string colorType)
    {
        if (drawSign == '0' || elementCount == 0)
        {
            Random randomSign = new Random();
                int a = randomSign.Next(1, 40);
                char randomDrawSign = Convert.ToChar(a);

            Random randomCount = new Random();
                int randomElementCount = randomCount.Next(4, 901);

                DrawTriangle.Triangle(randomDrawSign, emptySpace, randomElementCount, colorType);
        }

        else
        {
            char enteredDrawSign = drawSign;

            int enteredElementCount = elementCount;

            DrawTriangle.Triangle(enteredDrawSign, emptySpace, enteredElementCount, colorType);
        }
    }

    private static void Triangle(char triangleDrawSign, char emptySpace, int triangleElementCount, string colorType)
    {
        Colorize(colorType);
        
        double sqrt = Math.Sqrt(triangleElementCount);
       
        int rowCount = Convert.ToInt32(sqrt);
        
        int triangleBase = ((rowCount * 2) - 1);

        for (int m = 1, n = 1; m <= rowCount; m++, n--)
        {
            Console.WriteLine();

            for (int x = 1; x <= triangleBase + 2; x++)
            {
                if (x < (rowCount + n) || x > (rowCount + m))
                {
                    Console.Write(emptySpace);
                }

                else
                {
                    Console.Write(triangleDrawSign);
            
                    //Thread.Sleep(75);
                }
            }
        }

        Console.ResetColor();

        Console.WriteLine('\n');

        Console.WriteLine(
            "Трйгълника се състой от {0} знака от вид {1}, височина {2} знака, основа {3} знака, цвят '{4}'",
            triangleElementCount, triangleDrawSign, rowCount, triangleBase, colorType);

        ExitOrNew();
    }
    private static object Colorize(string colorType)
    {
        if (colorType == "white")
        {
            Console.ForegroundColor = ConsoleColor.White;
        }

        if (colorType == "red")
        {
            Console.ForegroundColor = ConsoleColor.Red;

        }

        if (colorType == "green")
        {
            Console.ForegroundColor = ConsoleColor.Green;
        }

        if (colorType == "random")
        {
            Random color = new Random();
            int colorNum = color.Next(0, 8);

            if (colorNum == 0){
                Console.ForegroundColor = ConsoleColor.Cyan;
            }
            else if (colorNum == 1){
                Console.ForegroundColor = ConsoleColor.DarkMagenta;
            }
            else if (colorNum == 2){
                Console.ForegroundColor = ConsoleColor.Blue;
            }
            else if (colorNum == 3){
                Console.ForegroundColor = ConsoleColor.DarkGreen;
            }
            else if (colorNum == 4){
                Console.ForegroundColor = ConsoleColor.DarkRed;
            }
            else if (colorNum == 5){
                Console.ForegroundColor = ConsoleColor.White;
            }
            else if (colorNum == 6){
                Console.ForegroundColor = ConsoleColor.Green;
            }
            else if (colorNum == 7){
                Console.ForegroundColor = ConsoleColor.Red;
            }
        }

        return Console.ForegroundColor;
    }
    private static void ExitOrNew()
    {
        Console.Write('\n');

        Console.WriteLine("За нов триъгълник въведи 'new' за изход от програмта 'exit'");

        string newExit = Console.ReadLine();

        if (newExit == "new")
        {
            Console.Clear();
            
            Main();
        }

        if (newExit == "exit")
        {
            Console.WriteLine("Довиждане!");
        }
    }
}

