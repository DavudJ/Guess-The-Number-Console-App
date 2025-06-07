# Guess The Number - C# Console Game

## Description

A simple C# console game where the computer randomly picks a number from 1 to 10, and you try to guess it. After each guess, the game tells you if the number is **prime/composite** and **even/odd** to help you out. If your guess is wrong, you can keep trying. After you guess correctly, you can play again or exit.

## How to Play

1. Run the program in your terminal.
2. Read the hints (prime/composite, even/odd).
3. Enter your guesses until you find the correct number.
4. After winning, decide if you want to play another round.

## Features

- Random number from 1 to 10 each round
- Hints about the number (prime/composite, even/odd)
- Input validation for guesses
- Option to play again after winning

## Requirements

- .NET SDK (any recent version)
- Terminal or console with Unicode support

here is the code:

    using System;
    using System.Text;
    
    namespace GuessTheNumber
    {
        internal class Program
        {
            static void Main(string[] args)
            {
                // Set encoding to support Unicode characters in console
                Console.OutputEncoding = Encoding.Unicode;
                Console.InputEncoding = Encoding.Unicode;
    
                Random random = new Random(); // Create random number generator
                int number = random.Next(1, 11); // Generate a number from 1 to 10
                string input;
                bool again = true; // Controls the main game loop
                bool cont = false; // Controls the input loop for playing again
                string userAnswer;
    
                Console.WriteLine("Hello! This game is called Guess the Number.");
                Console.WriteLine("Your goal is to guess the number I have in mind. I will give you some hints.");
    
                // Main game loop
                while (again == true)
                {
                    cont = false; // Reset continuation flag
                    Console.WriteLine("Ready? (type anything)");
    
                    Console.ReadLine(); // Wait for user to press Enter
                    Console.WriteLine("Let's go! I have chosen a number.");
    
                    // Give hint if number is prime
                    if (IsPrime(number))
                    {
                        Console.WriteLine("This number is prime.");
                    }
                    else
                    {
                        Console.WriteLine("This number is composite.");
                    }
    
                    // Give hint if number is even or odd
                    if (number % 2 == 0)
                    {
                        Console.WriteLine("This number is even.");
                    }
                    else
                    {
                        Console.WriteLine("This number is odd.");
                    }
    
                    Console.WriteLine("Guess the number from 1 to 10:");
    
                    // Guessing loop
                    while (true)
                    {
                        input = Console.ReadLine();
    
                        // Check if input is a valid integer
                        if (int.TryParse(input, out int userGuess))
                        {
                            // If guess is correct
                            if (userGuess == number)
                            {
                                Console.WriteLine("You guessed it! Congratulations!");
                                break; // Exit guessing loop
                            }
                            else
                            {
                                Console.WriteLine("Wrong guess! Try again.");
                            }
                        }
                        else
                        {
                            Console.WriteLine("Please enter a valid number!");
                        }
                    }
    
                    // Ask user if they want to play again
                    Console.WriteLine("Do you want to play again?");
                    while (!cont)
                    {
                        userAnswer = Convert.ToString(Console.ReadLine());
    
                        // Check user's answer
                        switch (userAnswer.ToLower())
                        {
                            case "yes":
                                again = true;
                                cont = true;
                                number = random.Next(1, 11); // Generate new number for next round
                                break;
                            case "no":
                                again = false;
                                cont = true;
                                break;
                            default:
                                Console.WriteLine("I didn't understand that.");
                                break;
                        }
                    }
                }
            }
    
            // Function to check if a number is prime
            static bool IsPrime(int number)
            {
                if (number < 2) return false;
    
                for (int i = 2; i <= Math.Sqrt(number); i++)
                {
                    if (number % i == 0)
                    {
                        return false;
                    }
                }
                return true;
            }
        }
    }
