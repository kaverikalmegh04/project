import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class BankManagementSystem {
    private static int accountNumberCounter = 1000;
    private Map<Integer, BankAccount> accounts;

    public BankManagementSystem() {
        this.accounts = new HashMap<>();
    }

    public int generateAccountNumber() {
        return accountNumberCounter++;
    }

    public void registerUser(String name, String address, String phoneNumber) {
        int accountNumber = generateAccountNumber();
        BankAccount account = new BankAccount(accountNumber, name, address, phoneNumber);
        accounts.put(accountNumber, account);
        System.out.println("User registered successfully. Account number: " + accountNumber);
    }

    public void generateToken(int accountNumber) {
        if (accounts.containsKey(accountNumber)) {
            BankAccount account = accounts.get(accountNumber);
            String token = TokenGenerator.generateToken();
            account.setToken(token);
            System.out.println("Token generated successfully. Token: " + token);
        } else {
            System.out.println("Account not found.");
        }
    }

    public void displayAccountDetails(int accountNumber) {
        if (accounts.containsKey(accountNumber)) {
            BankAccount account = accounts.get(accountNumber);
            System.out.println("Account details:");
            System.out.println(account);
        } else {
            System.out.println("Account not found.");
        }
    }

    public void updateAccountDetails(int accountNumber, String name, String address, String phoneNumber) {
        if (accounts.containsKey(accountNumber)) {
            BankAccount account = accounts.get(accountNumber);
            account.updateDetails(name, address, phoneNumber);
            System.out.println("Account details updated successfully.");
        } else {
            System.out.println("Account not found.");
        }
    }

    public void deleteAccount(int accountNumber) {
        if (accounts.containsKey(accountNumber)) {
            accounts.remove(accountNumber);
            System.out.println("Account deleted successfully.");
        } else {
            System.out.println("Account not found.");
        }
    }

    public static void main(String[] args) {
        BankManagementSystem bankSystem = new BankManagementSystem();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("Bank Management System Menu:");
            System.out.println("1. Register User");
            System.out.println("2. Generate Token");
            System.out.println("3. Display Account Details");
            System.out.println("4. Update Account Details");
            System.out.println("5. Delete Account");
            System.out.println("0. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume the newline character

            switch (choice) {
                case 1:
                    System.out.print("Enter name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter address: ");
                    String address = scanner.nextLine();
                    System.out.print("Enter phone number: ");
                    String phoneNumber = scanner.nextLine();
                    bankSystem.registerUser(name, address, phoneNumber);
                    break;
                case 2:
                    System.out.print("Enter account number: ");
                    int accNumber = scanner.nextInt();
                    bankSystem.generateToken(accNumber);
                    break;
                case 3:
                    System.out.print("Enter account number: ");
                    int accNum = scanner.nextInt();
                    bankSystem.displayAccountDetails(accNum);
                    break;
                case 4:
                    System.out.print("Enter account number: ");
                    int accNumb = scanner.nextInt();
                    System.out.print("Enter new name: ");
                    String newName = scanner.nextLine();
                    System.out.print("Enter new address: ");
                    String newAddress = scanner.nextLine();
                    System.out.print("Enter new phone number: ");
                    String newPhoneNumber = scanner.nextLine();
                    bankSystem.updateAccountDetails(accNumb, newName, newAddress, newPhoneNumber);
                    break;
                case 5:
                    System.out.print("Enter account number: ");
                    int accNo = scanner.nextInt();
                    bankSystem.deleteAccount(accNo);
                    break;
                case 0:
                    System.out.println("Exiting Bank Management System. Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please enter a valid option.");
            }
        }
    }
}

class BankAccount {
    private int accountNumber;
    private String name;
    private String address;
    private String phoneNumber;
    private String token;

    public BankAccount(int accountNumber, String name, String address, String phoneNumber) {
        this.accountNumber = accountNumber;
        this.name = name;
        this.address = address;
        this.phoneNumber = phoneNumber;
    }

    public void updateDetails(String name, String address, String phoneNumber) {
        this.name = name;
        this.address = address;
        this.phoneNumber = phoneNumber;
    }

    public void setToken(String token) {
        this.token = token;
    }

    @Override
    public String toString() {
        return "Account Number: " + accountNumber +
                "\nName: " + name +
                "\nAddress: " + address +
                "\nPhone Number: " + phoneNumber +
                "\nToken: " + token;
    }
}

class TokenGenerator {
    public static String generateToken() {
        // In a real-world scenario, implement a secure token generation logic
        return "GeneratedToken123";
    }
}
