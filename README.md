# Guess_the_number_game
import java.util.Random;
import java.util.Scanner;

public class NumberGuessingGame {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        int minRange = 1;
        int maxRange = 100;
        int attemptsLimit = 10; // Number of attempts allowed per round
        int round = 1;
        int score = 0;

        System.out.println("Welcome to the Number Guessing Game!");
        System.out.println("Guess a number between " + minRange + " and " + maxRange + ".");

        boolean playAgain = true;
        while (playAgain) {
            int targetNumber = random.nextInt(maxRange - minRange + 1) + minRange;
            System.out.println("\nRound " + round + ": New game! Guess the number.");

            int attempts = 0;
            boolean guessedCorrectly = false;

            while (attempts < attemptsLimit && !guessedCorrectly) {
                System.out.print("Attempt " + (attempts + 1) + "/" + attemptsLimit + ". Your guess: ");
                int guess = scanner.nextInt();

                if (guess < minRange || guess > maxRange) {
                    System.out.println("Your guess is out of the valid range (" + minRange + " to " + maxRange + "). Try again.");
                    continue;
                }

                if (guess < targetNumber) {
                    System.out.println("Too low! Try a higher number.");
                } else if (guess > targetNumber) {
                    System.out.println("Too high! Try a lower number.");
                } else {
                    System.out.println("Congratulations! You guessed the number " + targetNumber + " correctly in " + (attempts + 1) + " attempts.");
                    guessedCorrectly = true;
                    score += attempts + 1;
                }

                attempts++;
            }

            if (!guessedCorrectly) {
                System.out.println("Sorry, you've run out of attempts. The correct number was: " + targetNumber);
            }

            System.out.print("\nDo you want to play again? (yes/no): ");
            String playChoice = scanner.next().toLowerCase();

            if (!playChoice.equals("yes")) {
                playAgain = false;
            } else {
                round++;
            }
        }

        System.out.println("\nGame over! Your total score is: " + score);
        System.out.println("Thank you for playing!");
        scanner.close();
    }
}
