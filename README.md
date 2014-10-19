DrawTriangle
============

Console app that draws Triangle

using System;
using System.IO;
using System.Threading;

class MarketingInfo
{

    static void Main()
    {
        string directoryUsers = @"C:\MarketingInfo";

        string directoryPassWord = @"C:\MarketingInfo\PassWord";

        Directory.CreateDirectory(directoryUsers);

        Directory.CreateDirectory(directoryPassWord);
        
        Console.Clear();

        ConsoleSize();
        Console.Title = "Marketing Info ";
        
        AdministratorOrUser();
    }
    
    private static void User()
    {
        Console.Clear();

        ProgramLogo();

        Console.ResetColor();
        ColorBlueLine();
        PrintOnPosition(0, 46, "                                                            ");
        Console.ResetColor();
        PrintOnPosition(0, 48, "За връшане назад 'back'");
        PrintOnPosition(0, 49, "За запис на информацията 'save'");

        ColorYellowText();
        PrintOnPosition(0, 0, "ПОТРЕБИТЕЛСКА ЧАСТ");
        ColorBlueLine();
        PrintOnPosition(0, 1, "                                                            ");
        Console.ResetColor();

        string sobstvenoIme = "собствено име: ";

        Console.Write("Моля въдете вашето {0}", sobstvenoIme);

        ColorYellowText();

        string firstName = Console.ReadLine();

        if (firstName == "back")
        {
            Main();
        }

        if (firstName == "save")
        {
            Console.ResetColor();
            Console.WriteLine(@"'save' е командна дума /има още 5 въпроса за запис");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            //CheckTextInput(firstName);

            CheckTextInput2(firstName);

            CheckTextLenght(firstName);

            CheckNameLenght(firstName);
            
            Console.ResetColor();

            string familnoIme = "фамилно име: ";

            Console.Write("Моля въдете вашето {0}", familnoIme);

            ColorYellowText();

            string secondName = Console.ReadLine();

            if (secondName == "back")
            {
                User();
            }

            if (secondName == "save")
            {
                Console.ResetColor();
                Console.WriteLine(@"'save' е командна дума /има още 4 въпроса за запис");
                Thread.Sleep(2000);

                User();
            }

            else 
            {
                //CheckTextInput(secondName);

                CheckTextInput2(secondName);

                CheckTextLenght(secondName);

                CheckTextCoincide(firstName,secondName);

                CheckNameLenght(secondName);
                
                Console.ResetColor();

                string vuzrast = "възраст: ";

                Console.Write("Моля въдете вашата {0}", vuzrast);

                ColorYellowText();

                string ageString = Console.ReadLine();

                if (ageString == "back")
                {
                    User();
                }

                if (ageString == "save")
                {
                    Console.ResetColor();
                    Console.WriteLine(@"'save' е командна дума /има още 3 въпроса за запис");
                    Thread.Sleep(2000);

                    User();
                }

                else
                {
                    CheckNumberInput(ageString);

                    decimal ageInt = Convert.ToDecimal(ageString);
                    // int age = int.Parse(Console.ReadLine());

                    CheckAgeValue(ageInt);

                    Console.ResetColor();

                    string mujLiSte = "Мъж ли сте? - ";

                    Console.Write("{0} Моля отговорете с 'true' или 'false': ", mujLiSte);

                    ColorYellowText();

                    string genderString = Console.ReadLine();

                    if (genderString == "back")
                    {
                        User();
                    }

                    if (genderString == "save")
                    {
                        Console.ResetColor();
                        Console.WriteLine(@"'save' е командна дума /има още 2 въпроса за запис");
                        Thread.Sleep(2000);

                        User();
                    }

                    else if (genderString != "true" && genderString != "false" && genderString != "save" && genderString != "back")
                    {
                        Console.ResetColor();
                        Console.WriteLine("Моля отговорете с 'true' или 'false'");
                        Console.WriteLine("Изтриване...");
                        Thread.Sleep(2000);

                        User();
                    }

                    else 
                    {
                        bool genderBool = Convert.ToBoolean(genderString);

                        Console.ResetColor();

                            if (genderBool == true)
                            {
                                string genderMale = "Мъж";

                                Console.WriteLine("Вашият пол е {0}", genderMale);
                            }

                            if (genderBool == false)
                            {
                                string genderFemale = "Жена";

                                Console.WriteLine("Вашият пол е {0}", genderFemale);
                            }

                        string lichnaKarta = "лична карта: ";

                        Console.Write("Моля въдете номер на {0}", lichnaKarta);

                        ColorYellowText();

                        string idNumberString = Console.ReadLine();

                        if (idNumberString == "back")
                        {
                            User();
                        }

                        if (idNumberString == "save")
                        {
                            Console.ResetColor();
                            Console.WriteLine(@"'save' е командна дума /има още 1 въпрос за запис");
                            Thread.Sleep(2000);

                            User();
                        }

                        else
                        {
                            CheckNumberInput(idNumberString);

                            CheckIDLenght(idNumberString);

                            decimal idNumberInt = Convert.ToDecimal(idNumberString);

                            Console.ResetColor();

                            string kod = "код: ";

                            Console.Write("Вашият уникален {0}", kod);

                            ColorYellowText();

                            Random number = new Random();
                            int employeeNumber = number.Next(27560000, 27570000);

                            Console.Write(employeeNumber);

                            Console.Write('\n');

                            string backOrSave = Console.ReadLine();

                            if (backOrSave == "back")
                            {
                                User();
                            }

                            if (backOrSave == "save")
                            {
                                SaveFile(sobstvenoIme, firstName, familnoIme, 
                                 secondName, vuzrast, ageInt, mujLiSte, 
                                 genderBool, lichnaKarta, idNumberInt, kod, employeeNumber);
                            }
                        }
                    }
                }
            }
        }

        Console.ResetColor();
    }

    private static void SaveFile(string sobstvenoIme, string firstName, string familnoIme, 
                                 string secondName, string vuzrast, decimal ageInt, string mujLiSte, 
                                 bool genderBool, string lichnaKarta, decimal idNumberInt, string kod, int employeeNumber)
    {
        File.WriteAllText(@"C:\MarketingInfo\test.txt",
            sobstvenoIme + firstName + Environment.NewLine +
            familnoIme + secondName + Environment.NewLine +
            vuzrast + ageInt + Environment.NewLine +
            mujLiSte + genderBool + Environment.NewLine +
            lichnaKarta + idNumberInt + Environment.NewLine +
            kod + employeeNumber + Environment.NewLine);

        string txt = ".txt";  // file extention

        string uen = "_UEN_";  // abriviation for unique employee number

        File.Move(@"C:\MarketingInfo\test.txt", @"C:\MarketingInfo\" +
            firstName + '_' + secondName + uen + employeeNumber + txt);

        Console.ResetColor();
        Console.WriteLine("Данните за вас бяха запаметени");
        Thread.Sleep(2000);

        User();
    }

    private static void ColorYellowText()
    {
        Console.ForegroundColor = ConsoleColor.Yellow;
    }

    private static void ColorBlueLine()
    {
        Console.BackgroundColor = ConsoleColor.Blue;
    }

    private static void ProgramLogo()
    {
        Console.ForegroundColor = ConsoleColor.Gray;
        Console.BackgroundColor = ConsoleColor.White;
        PrintOnPosition(50, 40, "   M   "); 
        PrintOnPosition(50, 41, " A   R ");
        Console.ForegroundColor = ConsoleColor.DarkGreen;
        Console.BackgroundColor = ConsoleColor.Green;
        PrintOnPosition(50, 42, "K     E");
        PrintOnPosition(50, 43, " T   I ");
        Console.ForegroundColor = ConsoleColor.DarkRed;
        Console.BackgroundColor = ConsoleColor.Red;
        PrintOnPosition(50, 44, "  N G  ");
    }

    private static void AdministratorOrUser()
    {
        ProgramLogo();
        
        ColorBlueLine();
        PrintOnPosition(0, 47, "                                                            ");
        Console.ResetColor();
        PrintOnPosition(0, 49, "За изход 'exit'");

        ColorYellowText();
        PrintOnPosition(0, 0, "Добре дошли в MARKETING INFO");
        Console.ResetColor();
        ColorBlueLine();
        PrintOnPosition(0, 1, "                                                            ");
        Console.ResetColor();
        Console.Write("\n");

        PrintOnPosition(0, 2, "За въведжане на нов служител напишете 'new'");
        Console.WriteLine("За вход като администратор напишете 'admin'");
        ColorYellowText();

        string newAdmin = Console.ReadLine();

        if (newAdmin == "new")
        {
            Console.Clear();

            User();
        }

        if (newAdmin == "admin")
        {
            Console.Clear();
            
            Password();
        }

        if (newAdmin == "exit")
        {
            Console.Clear();
            
            ExitMessage();
        }

        if (newAdmin != "new" && newAdmin != "admin" && newAdmin != "exit")
        {
            Console.ResetColor();
            Console.WriteLine("Грешна команда");
            Thread.Sleep(2000);
            Console.Clear();

            AdministratorOrUser();
        }
    }

    private static void Password()
    {
        if (File.Exists(@"C:\MarketingInfo\PassWord\passWord.txt"))
        {
            ProgramLogo();

            ColorBlueLine();
            PrintOnPosition(0, 47, "                                                            ");
            Console.ResetColor();
            PrintOnPosition(0, 49, "За връшане назад 'back'");

            ColorYellowText();
            PrintOnPosition(0, 0, "ПАРОЛИ и ДОСТЪП");
            ColorBlueLine();
            PrintOnPosition(0, 1, "                                                            ");
            Console.ResetColor();
            PrintOnPosition(0, 2, "Въведете вашата парола");
            ColorYellowText();

            string passWord = Console.ReadLine();

            string checkPass = File.ReadAllText(@"C:\MarketingInfo\PassWord\passWord.txt");

            if (passWord == checkPass)
            {
                Console.Clear();

                Administrator();
            }

            if (passWord != checkPass && passWord != "back")
            {
                Console.ResetColor();
                Console.WriteLine("Грешна парола");
                Thread.Sleep(2000);
                Console.Clear();

                Password();
            }

            if (passWord == "back")
            {
                Console.Clear();

                AdministratorOrUser();
            }
        }

        else 
        {
            string defaultPassWord = "0000";

            File.WriteAllText(@"C:\MarketingInfo\PassWord\passWord.txt", defaultPassWord);

            Password();
        }
    }

    private static void Administrator()
    {
        ProgramLogo();
        Console.ResetColor();

        ColorBlueLine();
        PrintOnPosition(0, 45, "                                                            ");
        
        Console.ResetColor();
        PrintOnPosition(0, 47, "За връшане назад 'back'");
        PrintOnPosition(0, 48, @"За четене на файл 'read'");
        PrintOnPosition(0, 49, @"За смяна на парола 'pass'");
        
        ColorYellowText();
        PrintOnPosition(0, 0, "АДМИНИСТРАТИВНА ЧАСТ");
        
        ColorBlueLine();
        PrintOnPosition(0, 1, "                                                            ");
        Console.ResetColor();

        string filePath = @"C:\MarketingInfo";

        string[] files = Directory.GetFiles(filePath, "*.txt");

        int numberOfFiles = files.Length;

        Console.WriteLine("Налични са {0} досиета на служители", numberOfFiles);
  
            foreach (string file in files)
            {
                Console.WriteLine(file);
            }

        ColorYellowText();
        string backReadPass = Console.ReadLine();

        Console.ResetColor();

        if (backReadPass == "back")
        {
            Console.Clear();
            
            AdministratorOrUser();
        }

        if (backReadPass == "pass")
        {
            Console.Clear();

            PassWordChange();
        }

        if (backReadPass == "read" && numberOfFiles == 0)
        {

            Console.ResetColor();
            Console.WriteLine("Няма налични файлове за четене");
            Thread.Sleep(2000);
            Console.Clear();

            Administrator();
        }

        if (backReadPass == "read" && numberOfFiles >= 0)
        {
            ColorYellowText();
            string fileName = Console.ReadLine();
            Console.ResetColor();

            bool fileExists = File.Exists(@"C:\MarketingInfo\" + fileName);

            if (fileName == "passWord.txt")
            {
                Console.ResetColor();
                Console.WriteLine("Този файл е защитен");
                Thread.Sleep(2000);
                Console.Clear();

                Administrator();
            }

            if (fileExists == false)
            {
                Console.ResetColor();
                Console.WriteLine("Грешно име на файл");
                Thread.Sleep(2000);
                Console.Clear();

                Administrator();
            }

            else
            {
                string fileToRead = File.ReadAllText(@"C:\MarketingInfo\" + fileName);

                Console.WriteLine("Съдържанието на файла '{0}' е:", fileName);
                Console.WriteLine(fileToRead);

                ColorYellowText();
                string back = Console.ReadLine();

                Console.Clear();

                Administrator();
            }
        }

        if (backReadPass != "back" && backReadPass != "pass" && backReadPass != "read")
        {
            Console.ResetColor();
            Console.WriteLine("Грешна команда");
            Thread.Sleep(2000);
            Console.Clear();

            Administrator();
        }
    }

    private static void PassWordChange()
    {
        ProgramLogo();

        ColorBlueLine();
        PrintOnPosition(0, 47, "                                                            ");
        Console.ResetColor();
        PrintOnPosition(0, 49, "За връшане назад 'back'");

        ColorYellowText();
        PrintOnPosition(0, 0, "ПАРОЛИ и ДОСТЪП");
        ColorBlueLine();
        PrintOnPosition(0, 1, "                                                            ");
        Console.ResetColor();
        PrintOnPosition(0, 2, "Въведете вашата НАСТОЯЩА парола");
        ColorYellowText();

        string passWord = Console.ReadLine();

        string checkPass = File.ReadAllText(@"C:\MarketingInfo\PassWord\passWord.txt");

        if (passWord == checkPass)
        {
            Console.Clear();

            ProgramLogo();

            ColorBlueLine();
            PrintOnPosition(0, 47, "                                                            ");
            Console.ResetColor();

            ColorYellowText();
            PrintOnPosition(0, 0, "ПАРОЛИ и ДОСТЪП");
            ColorBlueLine();
            PrintOnPosition(0, 1, "                                                            ");
            Console.ResetColor();
            PrintOnPosition(0, 2, "Въведете вашата НОВА парола");
            ColorYellowText();

            string newPass = Console.ReadLine();

            //File.Delete(@"C:\MarketingInfo\PassWord\passWord.txt");

            //File.AppendAllText(@"C:\MarketingInfo\PassWord\passWord.txt", newPass);

            File.WriteAllText(@"C:\MarketingInfo\PassWord\passWord.txt", newPass);

            Console.ResetColor();
            Console.WriteLine("Паролата ви беше сменена успешно");
            Thread.Sleep(2000);

            Console.Clear();
            Administrator();
        }

        if (passWord != checkPass && passWord != "back")
        {
            Console.ResetColor();
            Console.WriteLine("Грешна парола");
            Thread.Sleep(2000);
            Console.Clear();

            PassWordChange();
        }

        if (passWord == "back")
        {
            Console.Clear();

            Administrator();
        }

    }

    private static void CheckNumberInput(string inputNumber)
    {
        decimal a;

        bool checkNumInput = decimal.TryParse(inputNumber, out a);

        if (checkNumInput == false)
        {
            Console.ResetColor();
            Console.WriteLine("Моля въведи число");
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    private static void CheckAgeValue(decimal inputAge)
    {
        if (inputAge <= 18 || inputAge >= 100)
        {
            Console.ResetColor();
            Console.WriteLine("Възрастта ви може да е от 18 до 100 год");
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    //private static void CheckTextInput(string inputText) // замесетен от CheckTextLenght2 който засича и цифри смесени с букви
    //{
    //    int b;

    //    bool checkTxtInput = int.TryParse(inputText, out b);

    //    if (checkTxtInput == true)
    //    {
    //        Console.ResetColor();
    //        Console.WriteLine("Моля въведи букви");
    //        Console.WriteLine("Изтриване...");
    //        Thread.Sleep(2000);

    //        User();
    //    }

    //    else
    //    {
    //        return;
    //    }
    //}

    private static void CheckTextCoincide(string firstName, string secondName)
    {
        if (firstName == secondName)
        {
            Console.ResetColor();
            Console.WriteLine("Имената ви неможе да съвпадат");
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    private static void CheckTextLenght(string textLenght)
    {
        int lenght = textLenght.Length;

        if (lenght <= 2)
        {
            Console.ResetColor();
            Console.WriteLine("Неможе да съдържа само 2 символа");
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    private static void CheckIDLenght(string idLenght)
    {
        int lenght = idLenght.Length;

        if (lenght < 7 || lenght > 7)
        {
            Console.ResetColor();
            Console.WriteLine("Трябва да съдържа 7 цифри");
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    private static void CheckNameLenght(string nameLenght)
    {
        int lenght = nameLenght.Length;

        if (lenght > 12)
        {
            Console.ResetColor();
            Console.WriteLine("Неможе да съдържа {0} символа, максимум 12", lenght);
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    private static void CheckTextInput2(string inputText)
    {
        string a1 = "1"; string a2 = "2"; string a3 = "3"; string a4 = "4"; string a5 = "5";
        string a6 = "6"; string a7 = "7"; string a8 = "8"; string a9 = "9";
                
        bool checkTxtInput;

        checkTxtInput = inputText.Contains(a1) || inputText.Contains(a2) || inputText.Contains(a3) || inputText.Contains(a4) || inputText.Contains(a5)
            || inputText.Contains(a6) || inputText.Contains(a7) || inputText.Contains(a8) || inputText.Contains(a9);

        if (checkTxtInput == true)
        {
            Console.ResetColor();
            Console.WriteLine("Моля въведи само букви");
            Console.WriteLine("Изтриване...");
            Thread.Sleep(2000);

            User();
        }

        else
        {
            return;
        }
    }

    private static void PrintOnPosition(int x, int y, string text)
    {
        Console.SetCursorPosition(x, y);
        Console.WriteLine(text);
    }

    private static void ConsoleSize()
    {
        Console.BufferHeight = Console.WindowHeight = 50;
        Console.BufferWidth = Console.WindowWidth = 60;
    }

    private static void ExitMessage()
    {
        ColorBlueLine();
        PrintOnPosition(0, 47, "                                                            ");
        Console.ResetColor();
        PrintOnPosition(0, 49, " ");
        
        ProgramLogo();
        Console.ResetColor();

        ColorYellowText();
        PrintOnPosition(0, 0, "Довиждане!");
        Console.ResetColor();

        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}

