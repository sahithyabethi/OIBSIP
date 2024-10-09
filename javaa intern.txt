import java.util.Scanner;
public class ATMInterface {

    private static double balance = 1000.00;
    private static final String USER_ID = "user123";
    private static final String USER_PIN = "1234";

    
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        if (login()) {
            showMenu();
        } else {
            System.out.println("Invalid User ID or PIN. Access Denied!");
        }
    }

    private static boolean login() {
        System.out.println("Welcome to the ATM!");
        System.out.print("Enter User ID: ");
        String enteredUserId = scanner.nextLine();
        System.out.print("Enter User PIN: ");
        String enteredPin = scanner.nextLine();

        return enteredUserId.equals(USER_ID) && enteredPin.equals(USER_PIN);
    }

    private static void showMenu() {
        int choice;

        do {
            System.out.println("\nATM Menu:");
            System.out.println("1. Transactions History");
            System.out.println("2. Withdraw");
            System.out.println("3. Deposit");
            System.out.println("4. Transfer");
            System.out.println("5. Quit");
            System.out.print("Choose an option: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    transactionHistory();
                    break;
                case 2:
                    withdraw();
                    break;
                case 3:
                    deposit();
                    break;
                case 4:
                    transfer();
                    break;
                case 5:
                    System.out.println("Exiting... Thank you for using the ATM!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 5);
    }

    private static void transactionHistory() {
        System.out.println("Transaction History:");
        System.out.println("1. Withdraw: $100");
        System.out.println("2. Deposit: $500");
        System.out.println("Current Balance: $" + balance);
    }

    private static void withdraw() {
        System.out.print("Enter amount to withdraw: ");
        double amount = scanner.nextDouble();

        if (amount <= balance) {
            balance -= amount;
            System.out.println("Successfully withdrawn: $" + amount);
            System.out.println("New balance: $" + balance);
        } else {
            System.out.println("Insufficient funds.");
        }
    }

    private static void deposit() {
        System.out.print("Enter amount to deposit: ");
        double amount = scanner.nextDouble();
        balance += amount;
        System.out.println("Successfully deposited: $" + amount);
        System.out.println("New balance: $" + balance);
    }

    private static void transfer() {
        System.out.print("Enter amount to transfer: ");
        double amount = scanner.nextDouble();

        if (amount <= balance) {
            balance -= amount;
            System.out.println("Successfully transferred: $" + amount + " to recipient.");
            System.out.println("New balance: $" + balance);
        } else {
            System.out.println("Insufficient funds.");
        }
    }
}