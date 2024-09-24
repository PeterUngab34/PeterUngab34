import javax.swing.JOptionPane;
import java.util.ArrayList;

public class Kupal {
    public static void main(String[] args) {
        System.out.println("WELCOME TO MY STORE\nREFLEX ESPORTS");

        while (true) {
            boolean continueShopping = order();
            if (!continueShopping) {
                System.out.println("Thank you for visiting!");
                break; 
            }
        }
    }

    public static boolean order() {
        double total = 0;
        double pay;
        String again;

        
        ArrayList<String> orderedItems = new ArrayList<>();
        ArrayList<Integer> orderedQuantities = new ArrayList<>();
        ArrayList<Double> orderedPrices = new ArrayList<>();
        
        double[] prices = {50.00, 35.00, 25.00, 45.00, 150.00};
        String[] items = {"Burger", "Hotdog", "Ice Cream", "Smoothie", "Steak"};

        do {
            String menu = "==========MENU ITEMS==========\n" +
                          "1. Burger - 50.00\n" +
                          "2. Hotdog - 35.00\n" +
                          "3. Ice Cream - 25.00\n" +
                          "4. Smoothie - 45.00\n" +
                          "5. Steak - 150.00\n" +
                          "6. EXIT\n" +
                          "Select an item (1-5) or press 6 to EXIT:";
            String input = JOptionPane.showInputDialog(menu);
            int choice = Integer.parseInt(input);

            if (choice >= 1 && choice <= 5) {
                String qtyInput = JOptionPane.showInputDialog("You chose " + items[choice - 1] +
                                                                "\nHow many would you like to buy?");
                int quantity = Integer.parseInt(qtyInput);

                
                orderedItems.add(items[choice - 1]);
                orderedQuantities.add(quantity);
                orderedPrices.add(prices[choice - 1] * quantity);

                total += quantity * prices[choice - 1];
                JOptionPane.showMessageDialog(null, "Total so far: " + total);
            } else if (choice == 6) {
                return false;  
            } else {
                JOptionPane.showMessageDialog(null, "Invalid choice. Please select between 1 to 6.");
            }

            again = JOptionPane.showInputDialog("Would you like to buy more? (Y/N):");
        } while (again.equalsIgnoreCase("Y"));

        
        double discount = 0;
        if (total >= 700) {
            discount = total * 0.05;
            total -= discount;
            JOptionPane.showMessageDialog(null, "Discount applied: " + discount);
        }

        
        StringBuilder receipt = new StringBuilder();
        receipt.append("========== RECEIPT ==========\n");
        for (int i = 0; i < orderedItems.size(); i++) {
            receipt.append(orderedItems.get(i)).append(" x")
                   .append(orderedQuantities.get(i))
                   .append(" = ")
                   .append(String.format("%.2f", orderedPrices.get(i)))
                   .append("\n");
        }
        if (discount > 0) {
            receipt.append("Discount: ").append(String.format("%.2f", discount)).append("\n");
        }
        receipt.append("Total: ").append(String.format("%.2f", total)).append("\n");
        receipt.append("=============================\n");

        JOptionPane.showMessageDialog(null, receipt.toString());

        
        if (total > 0) {
            for (int attempts = 0; attempts < 3; attempts++) {
                String payInput = JOptionPane.showInputDialog("Total amount to pay: " + total + "\nEnter payment amount:");
                pay = Double.parseDouble(payInput);
                pay = Math.round(pay * 100.0) / 100.0;

                if (pay < total) {
                    JOptionPane.showMessageDialog(null, "Not enough payment. Please provide more money.");
                    total -= pay;
                    JOptionPane.showMessageDialog(null, "Remaining balance: " + total);
                } else {
                    double change = pay - total;
                    JOptionPane.showMessageDialog(null, "Payment successful! Your change: " + Math.round(change * 100.0) / 100.0);
                    total = 0;
                    break; 
                }

                if (attempts == 2) {
                    JOptionPane.showMessageDialog(null, "Payment failed after 3 attempts. Order voided.");
                    return true; 
                }
            }
        } else {
            JOptionPane.showMessageDialog(null, "No items purchased.");
        }

        
        String pet = JOptionPane.showInputDialog("Enter Pet Name:");
        String number = JOptionPane.showInputDialog("Enter a Number:");
        int ul = Integer.parseInt(number);
        String number1 = JOptionPane.showInputDialog("Enter a Double Number:");
        double uls = Double.parseDouble(number1);

        JOptionPane.showMessageDialog(null, "Number + 100: " + (ul + 100));
        JOptionPane.showMessageDialog(null, "Double Number + 100: " + (uls + 100));
        JOptionPane.showMessageDialog(null, pet + "\nWow, Pet!");

        return true;  
    }
}
