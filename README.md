# 8Ball

using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Threading;
using System.Speech.Synthesis;
namespace Magic8Ball
{
    /// <summary>
    /// entry point for magic 8 ball program
    /// </summary>
    class Program
    {
        private static SpeechSynthesizer synth = new SpeechSynthesizer();

        static void Main(string[] args)
        {
            // This will greet the user, tell them the application, ask them to type a question or quit to exit
            synth.Rate = 2;
            synth.Speak("Hello. Welcome to the magic 8 ball application.  Please ask a question or type quit to exit.");

            // Preserve current console text color
            ConsoleColor oldColor = Console.ForegroundColor;

            TellPeopleWhatProgramThisIs();

            // create a randomizer object
            Random randomObject = new Random();

            // Loop forever!!!
            while (true)
            {
                string questionString = GetQuestionFromUser();

                int numberOfSecondsTosleep = randomObject.Next(5) + 1;
                Console.WriteLine("Thinking about your question, stand by...");
                Thread.Sleep(numberOfSecondsTosleep * 1000);

                if (questionString.Length == 0)
                {
                    Console.WriteLine("You need to type a question fool");
                    continue;
                }

                // See if the user typed 'quit' as the question
                if (questionString.ToLower() == "quit")
                {
                    Console.WriteLine("What?! You want to leave me?! You will now be Rick rolled!");
                    synth.Speak("What?! You want to leave me?! You will now be Rick rolled!");
                    OpenWebsite("https://www.youtube.com/watch?v=dQw4w9WgXcQ");
                    break;
                }

                // If the user insults with 'you suck' smack them and close
                if (questionString.ToLower() == "you suck")
                {
                    Console.WriteLine("You suck even more!");
                    break;
                }

                // Get a random number
                int randomNumber = randomObject.Next(4);

                Console.ForegroundColor = (ConsoleColor)randomNumber;

                // Use random number to determine response
                switch (randomNumber)
                {
                    case 0: 
                        {
                            Console.WriteLine("YES!");
                            break;
                        }
                    case 1:
                        {
                            Console.WriteLine("NO!");
                            break;
                        }
                    case 2:
                        {
                            Console.WriteLine("HELL NO!");
                            break;
                        }
                    case 3:
                        {
                            Console.WriteLine("OMG YES!");
                            break;
                        }
                }
            }

            //Cleaning up
            Console.ForegroundColor = oldColor;
        }

        /// <summary>
        /// This will print the name of the program and who created it
        /// to the console
        /// </summary>
        static void TellPeopleWhatProgramThisIs()
        {
            // Change console text color
            Console.ForegroundColor = ConsoleColor.Red;
            Console.Write("M");
            Console.ForegroundColor = ConsoleColor.Blue;
            Console.WriteLine("agic 8 ball (by: Robert)");
        }

        /// <summary>
        /// This function will return the text that user types
        /// </summary>
        /// <returns></returns>
        static string GetQuestionFromUser()
        {
            // This block of code will ask the user for a question
            // and store the questoin text in questoinString variable
            Console.ForegroundColor = ConsoleColor.White;
            Console.Write("Ask a question?: ");
            Console.ForegroundColor = ConsoleColor.Gray;
            string questionString = Console.ReadLine();

            return questionString;

        }
        
        // Open a website
        public static void OpenWebsite(string URL)
        {
            Process firstProcess = new Process();
            firstProcess.StartInfo.FileName = "firefox.exe";
            firstProcess.StartInfo.Arguments = URL;
            firstProcess.StartInfo.WindowStyle = ProcessWindowStyle.Maximized;
            firstProcess.Start();
        }
    }
}
