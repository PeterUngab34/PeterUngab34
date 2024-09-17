import java.util.Scanner;

public class PETERPAULUNGAB {

    public static void main(String[] args) {
        System.out.println("WELCOME TO MY STORE\n REFLEX ESPORTS");

        while (true) {
            order();
        }
    }

    public static void order() {
        Scanner input = new Scanner(System.in);

        int choice;
        int quantity;
        double total = 0;
        double pay;
        String again;

        double[] prices = {50.00, 35.00, 25.00, 45.00, 150.00};
        String[] items = {"Burger", "Hotdog", "Ice Cream", "Smoothie", "Steak"};

        do {
            System.out.println("==========MENU ITEMS==========");
            System.out.println("1. Burger - 50.00\n" +
                               "2. Hotdog - 35.00\n" +
                               "3. Ice Cream - 25.00\n" +
                               "4. Smoothie - 45.00\n" +
                               "5. Steak - 150.00\n" +
                               "6. EXIT");

            System.out.println("Select an item (1-5) or press 6 to EXIT:");
            choice = input.nextInt();

            if (choice >= 1 && choice <= 5) {
                System.out.println("You chose " + items[choice - 1]);
                System.out.print("How many would you like to buy? ");
                quantity = input.nextInt();

                total += quantity * prices[choice - 1];
                System.out.println("Total so far: " + total);

            } else if (choice == 6) {
                System.out.println("Exiting the store.");
                break;
            } else {
                System.out.println("Invalid choice. Please select between 1 to 6.");
            }

            System.out.print("Would you like to buy more? (Y/N): ");
            again = input.next();

        } while (again.equalsIgnoreCase("Y"));

        if (total > 0) {
            System.out.println("Total amount to pay: " + total);

            do {
                System.out.print("Enter payment amount: ");
                pay = input.nextDouble();

                pay = Math.round(pay * 100.0) / 100.0;

                if (pay < total) {
                    System.out.println("Not enough payment. Please provide more money.");
                    total -= pay;  
                    System.out.println("Remaining balance: " + total);
                } else {
                    double change = pay - total;
                    System.out.println("Payment successful! Your change: " + Math.round(change * 100.0) / 100.0);
                    total = 0;  
                }
            } while (total > 0);

        } else {
            System.out.println("No items purchased.");
        }
    }
}
