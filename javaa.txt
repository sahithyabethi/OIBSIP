import java.util.Random;
import java.util.Scanner;
public class GuessTheNumber {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        int maxRounds = 5; 
        int maxAttempts = 7; 
        int totalScore = 0;  

        System.out.println("Welcome to the Guess the Number Game!");
        System.out.println("You have " + maxRounds + " rounds to play. Points are awarded based on attempts.");
        
        for (int round = 1; round <= maxRounds; round++) {
            System.out.println("\nRound " + round + ":");
            int numberToGuess = random.nextInt(100) + 1;
            int attempts = 0;
            boolean hasWon = false;
            
            while (attempts < maxAttempts) {
                System.out.print("Guess the number (1-100): ");
                int userGuess = scanner.nextInt();
                attempts++;
                
                if (userGuess == numberToGuess) {
                    hasWon = true;
                    int points = maxAttempts - attempts + 1;  
                    totalScore += points;
                    System.out.println("Congratulations! You've guessed the number in " + attempts + " attempts.");
                    System.out.println("You earned " + points + " points this round.");
                    break;
                } else if (userGuess > numberToGuess) {
                    System.out.println("Too high!");
                } else {
                    System.out.println("Too low!");
                }
            }
            
            if (!hasWon) {
                System.out.println("Sorry, you've used all your attempts. The correct number was " + numberToGuess + ".");
            }
            
            System.out.println("Current score: " + totalScore);
        }
        
        System.out.println("\nGame over! Your total score is: " + totalScore);
        scanner.close();
    }
}