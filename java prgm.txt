import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class OnlineReservationSystem {
    private static Map<String, String> users = new HashMap<>();
    private static Map<String, String> reservations = new HashMap<>();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        initializeUsers(); 
        System.out.println("Welcome to the Online Reservation System");

        if (login()) {
            int option;
            do {
                System.out.println("\nSelect an option:");
                System.out.println("1. Make a Reservation");
                System.out.println("2. Cancel a Reservation");
                System.out.println("3. Exit");
                option = scanner.nextInt();
                scanner.nextLine();  

                switch (option) {
                    case 1:
                        makeReservation();
                        break;
                    case 2:
                        cancelReservation();
                        break;
                    case 3:
                        System.out.println("Thank you for using the system.");
                        break;
                    default:
                        System.out.println("Invalid option, try again.");
                }
            } while (option != 3);
        }
    }

    private static void initializeUsers() {
        users.put("user1", "sahi1234");
        users.put("user2", "likki1234");
    }

    private static boolean login() {
        System.out.print("Enter your login ID: ");
        String loginID = scanner.nextLine();
        System.out.print("Enter your password: ");
        String password = scanner.nextLine();

        if (users.containsKey(loginID) && users.get(loginID).equals(password)) {
            System.out.println("Login successful!");
            return true;
        } else {
            System.out.println("Invalid login ID or password.");
            return false;
        }
    }

    private static void makeReservation() {
        System.out.print("Enter Train Number: ");
        String trainNumber = scanner.nextLine();
        System.out.print("Enter Train Name: ");
        String trainName = scanner.nextLine();
        System.out.print("Enter Place of Departure: ");
        String departure = scanner.nextLine();
        System.out.print("Enter Destination: ");
        String destination = scanner.nextLine();
        System.out.print("Enter Journey Date: ");
        String date = scanner.nextLine();

        String reservationDetails = "Train Number: " + trainNumber + 
                                    ", Train Name: " + trainName + 
                                    ", From: " + departure + 
                                    ", To: " + destination + 
                                    ", Date: " + date;
        String pnr = "PNR" + (int)(Math.random() * 10000);  
        reservations.put(pnr, reservationDetails);
        System.out.println("Reservation successful. Your PNR is: " + pnr);
    }
    private static void cancelReservation() {
        System.out.print("Enter your PNR Number: ");
        String pnr = scanner.nextLine();
        
        if (reservations.containsKey(pnr)) {
            System.out.println("Reservation Details: " + reservations.get(pnr));
            System.out.print("Do you want to cancel this reservation? (yes/no): ");
            String confirm = scanner.nextLine();
            if (confirm.equalsIgnoreCase("yes")) {
                reservations.remove(pnr);
                System.out.println("Reservation cancelled successfully.");
            } else {
                System.out.println("Cancellation aborted.");
            }
        } else {
            System.out.println("PNR not found.");
        }
    }
}