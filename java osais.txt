import java.util.*;

class User {
    private String username;
    private String password;
    private String name;
    private String email;

    public User(String username, String password, String name, String email) {
        this.username = username;
        this.password = password;
        this.name = name;
        this.email = email;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    public void updateProfile(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public void updatePassword(String newPassword) {
        this.password = newPassword;
    }
}

class MCQ {
    private String question;
    private String[] options;
    private int correctOption;

    public MCQ(String question, String[] options, int correctOption) {
        this.question = question;
        this.options = options;
        this.correctOption = correctOption;
    }

    public String getQuestion() {
        return question;
    }

    public String[] getOptions() {
        return options;
    }

    public boolean checkAnswer(int selectedOption) {
        return selectedOption == correctOption;
    }
}

public class OnlineExamination {
    private static HashMap<String, User> users = new HashMap<>();
    private static User loggedInUser = null;
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        System.out.println("Welcome to Online Examination System");

        // Initialize some users
        users.put("user1", new User("user1", "sahi2004", "Sahithya", "sahithya1@example.com"));
        users.put("user2", new User("user2", "likki2002", "Likitha", "likitha@example.com"));

        while (true) {
            System.out.println("\nMain Menu");
            System.out.println("1. Login");
            System.out.println("2. Exit");

            int choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            if (choice == 1) {
                login();
            } else if (choice == 2) {
                System.out.println("Exiting the system. Goodbye!");
                break;
            } else {
                System.out.println("Invalid option. Please try again.");
            }
        }
    }

    public static void login() {
        System.out.print("Enter Username: ");
        String username = scanner.nextLine();
        System.out.print("Enter Password: ");
        String password = scanner.nextLine();

        if (users.containsKey(username) && users.get(username).getPassword().equals(password)) {
            loggedInUser = users.get(username);
            System.out.println("Login successful!");
            userMenu();
        } else {
            System.out.println("Invalid credentials.");
        }
    }

    public static void userMenu() {
        while (true) {
            System.out.println("\nUser Menu");
            System.out.println("1. Update Profile");
            System.out.println("2. Change Password");
            System.out.println("3. Start Exam");
            System.out.println("4. Logout");

            int choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    updateProfile();
                    break;
                case 2:
                    changePassword();
                    break;
                case 3:
                    startExam();
                    return; // After exam, logout automatically
                case 4:
                    logout();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    public static void updateProfile() {
        System.out.print("Enter new Name: ");
        String name = scanner.nextLine();
        System.out.print("Enter new Email: ");
        String email = scanner.nextLine();
        loggedInUser.updateProfile(name, email);
        System.out.println("Profile updated successfully.");
    }

    public static void changePassword() {
        System.out.print("Enter new Password: ");
        String newPassword = scanner.nextLine();
        loggedInUser.updatePassword(newPassword);
        System.out.println("Password updated successfully.");
    }

    public static void startExam() {
        MCQ[] questions = {
            new MCQ("What is the capital of France?", new String[]{"1. Berlin", "2. Madrid", "3. Paris", "4. Rome"}, 3),
            new MCQ("Which planet is known as the Red Planet?", new String[]{"1. Earth", "2. Mars", "3. Jupiter", "4. Venus"}, 2),
            new MCQ("What is the boiling point of water?", new String[]{"1. 50°C", "2. 100°C", "3. 150°C", "4. 200°C"}, 2)
        };

        int score = 0;
        TimerTask task = new TimerTask() {
            @Override
            public void run() {
                System.out.println("\nTime is up! Exam submitted automatically.");
                System.out.println("You scored: " + score + "/" + questions.length);
                logout();
                System.exit(0);
            }
        };

        Timer timer = new Timer();
        timer.schedule(task, 30000); // Auto submit after 30 seconds

        for (MCQ question : questions) {
            System.out.println(question.getQuestion());
            for (String option : question.getOptions()) {
                System.out.println(option);
            }
            System.out.print("Select option: ");
            int selectedOption = scanner.nextInt();

            if (question.checkAnswer(selectedOption)) {
                score++;
            }
        }

        timer.cancel(); // Cancel timer if exam is submitted manually
        System.out.println("You scored: " + score + "/" + questions.length);
    }

    public static void logout() {
        loggedInUser = null;
        System.out.println("Logged out successfully.");
    }
}