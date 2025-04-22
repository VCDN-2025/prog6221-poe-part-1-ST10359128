using System;
using System.IO;
using System.Media;
using System.Threading;

namespace CybersecurityAwarenessBot
{
    class Program
    {
        static void Main(string[] args)
        {
            // Play Voice Greeting
            PlayVoiceGreeting();

            // Display ASCII Art
            DisplayAsciiArt();

            // Greet User
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("==================================================");
            Console.WriteLine("       WELCOME TO THE CYBERSECURITY AWARENESS BOT ");
            Console.WriteLine("==================================================");
            Console.ResetColor();

            Console.Write("Please enter your name: ");
            string name = Console.ReadLine();
            if (string.IsNullOrWhiteSpace(name))
                name = "Friend";

            TypeWrite($"Hi {name}, I'm your Cybersecurity Assistant! You can ask me about phishing, password safety, or safe browsing.\n");

            // Chat Loop
            while (true)
            {
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("\nAsk me something (or type 'exit' to quit):");
                Console.ResetColor();

                string input = Console.ReadLine()?.ToLower();

                if (string.IsNullOrWhiteSpace(input))
                {
                    Console.WriteLine("Please enter a valid question.");
                    continue;
                }

                if (input == "exit")
                {
                    Console.WriteLine("Stay safe online! Goodbye!");
                    break;
                }

                RespondToInput(input);
            }
        }

        static void PlayVoiceGreeting()
        {
            try
            {
                SoundPlayer player = new SoundPlayer("Resources/greeting.wav");
                player.PlaySync();
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error playing voice greeting: " + ex.Message);
            }
        }

        static void DisplayAsciiArt()
        {
            try
            {
                string art = File.ReadAllText("Resources/ascii.txt");
                Console.ForegroundColor = ConsoleColor.Cyan;
                Console.WriteLine(art);
                Console.ResetColor();
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error displaying ASCII art: " + ex.Message);
            }
        }

        static void TypeWrite(string text, int delay = 35)
        {
            foreach (char c in text)
            {
                Console.Write(c);
                Thread.Sleep(delay);
            }
            Console.WriteLine();
        }

        static void RespondToInput(string input)
        {
            switch (input)
            {
                case "how are you":
                case "how are you?":
                    Console.WriteLine("I'm doing great! Always on the lookout for cyber threats.");
                    break;
                case "what's your purpose":
                case "what is your purpose":
                    Console.WriteLine("My purpose is to teach you how to stay safe in every way online.");
                    break;
                case "what can i ask you about":
                case "what can i ask you about?":
                    Console.WriteLine("You can ask me about password safety, phishing, and safe browsing.");
                    break;
                case "phishing":
                    Console.WriteLine("Phishing is when attackers trick you into giving personal info. Always verify emails before clicking links.");
                    break;
                case "password safety":
                    Console.WriteLine("Use strong, unique passwords. Never reuse passwords across sites. Use a password manager if needed.");
                    break;
                case "safe browsing":
                    Console.WriteLine("Avoid suspicious websites, check for HTTPS, and keep your browser updated.");
                    break;
                default:
                    Console.WriteLine("I didn't quite understand that. Could you rephrase?");
                    break;
            }
        }
    }
}

