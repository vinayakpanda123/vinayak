# simple java
    import java.util.Scanner;

     public class PizzaRestaurantj {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Pizza types and their prices
        String[] pizzaTypes = {"Margherita", "Pepperoni", "BBQ Chicken", "Vegetarian"};
        double[] pizzaPrices = {8.99, 9.99, 10.99, 7.99};

        // Display pizza options
        System.out.println("Welcome to the Pizza Restaurant!");
        System.out.println("Available Pizzas:");
        for (int i = 0; i < pizzaTypes.length; i++) {
            System.out.println((i + 1) + ". " + pizzaTypes[i] + " - $" + pizzaPrices[i]);
        }

        // Prompt user for pizza choice
        System.out.print("Select the pizza type (1-" + pizzaTypes.length + "): ");
        int pizzaChoice = scanner.nextInt() - 1;

        // Prompt user for size
        System.out.print("Enter the size (Small, Medium, Large): ");
        String size = scanner.next();

        // Prompt user for toppings
        System.out.print("Enter toppings (comma-separated): ");
        scanner.nextLine(); // Consume the newline
        String toppings = scanner.nextLine();

        // Prompt user for quantity
        System.out.print("Enter the quantity: ");
        int quantity = scanner.nextInt();

        // Calculate total price
        double totalPrice = pizzaPrices[pizzaChoice] * quantity;

        // Display order summary
        System.out.println("\nOrder Summary:");
        System.out.println("Pizza Type: " + pizzaTypes[pizzaChoice]);
        System.out.println("Size: " + size);
        System.out.println("Toppings: " + toppings);
        System.out.println("Quantity: " + quantity);
        System.out.printf("Total Price: $%.2f\n", totalPrice);

        // Close the scanner
        scanner.close();
    }
    }

 #Array

      import java.util.HashMap;
      import java.util.Scanner;

    class Pizza {
    private String type; // Type of the pizza
    private String size; // Size of the pizza
    private String[] toppings; // Array to store toppings
    private int toppingCount; // Count of toppings added
    private double basePrice; // Base price of the pizza

    // Constructor that initializes the type, size, and base price
    public Pizza(String type, String size) {
        this.type = type;
        this.size = size;
        this.toppings = new String[10]; // Assuming a max of 10 toppings
        this.toppingCount = 0; // Initialize topping count
        this.basePrice = calculateBasePrice(type, size); // Calculate base price based on type and size
    }

    // Method to calculate the base price based on the type and size
    private double calculateBasePrice(String type, String size) {
        double typeBasePrice;
        switch (type.toLowerCase()) {
            case "margherita":
                typeBasePrice = 8.00;
                break;
            case "pepperoni":
                typeBasePrice = 9.00;
                break;
            case "veggie":
                typeBasePrice = 8.50;
                break;
            case "bbq chicken":
                typeBasePrice = 10.00;
                break;
            default:
                typeBasePrice = 0.00; // Return 0 if type is invalid
        }

        // Adjust base price based on size
        double sizeMultiplier;
        switch (size.toLowerCase()) {
            case "small":
                sizeMultiplier = 1.0; // No extra charge for small
                break;
            case "medium":
                sizeMultiplier = 1.25; // 25% extra for medium
                break;
            case "large":
                sizeMultiplier = 1.5; // 50% extra for large
                break;
            default:
                sizeMultiplier = 0.0; // Return 0 if size is invalid
        }

        return typeBasePrice * sizeMultiplier; // Calculate total base price
    }

    // Method to add a topping to the pizza
    public void addTopping(String topping) {
        if (toppingCount < toppings.length) {
            toppings[toppingCount++] = topping; // Add topping to the array
        } else {
            System.out.println("Maximum toppings reached.");
        }
    }

    // Method to calculate the total price of the pizza
    public double calculateTotalPrice() {
        return basePrice + (toppingCount * 1.50); // Each topping costs $1.50
    }

    // Override toString method to display pizza details
    @Override
    public String toString() {
        StringBuilder toppingList = new StringBuilder();
        for (int i = 0; i < toppingCount; i++) {
            toppingList.append(toppings[i]);
            if (i < toppingCount - 1) {
                toppingList.append(", ");
            }
        }
        return "Pizza Type: " + type + ", Size: " + size + ", Toppings: " + toppingList.toString() + ", Total Price: $" + String.format("%.2f", calculateTotalPrice());
    }
    }

    public class PizzaRestaurant {
    // Array to store available toppings
    private static final String[] availableToppings = {
        "pepperoni", "mushrooms", "onions", "sausage", 
        "bacon", "extra cheese", "black olives", 
        "green peppers", "pineapple", "spinach"
    };

    // Array to store available pizza types
    private static final String[] availablePizzaTypes = {
        "Margherita", "Pepperoni", "Veggie", "BBQ Chicken"
    };

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // Scanner for user input
        System.out.println("Welcome to the Pizza Restaurant!");

        // Prompt user to choose pizza type
        System.out.println("Available pizza types: ");
        for (String pizzaType : availablePizzaTypes) {
            System.out.println("- " + pizzaType);
        }
        System.out.print("Choose pizza type: ");
        String type = scanner.nextLine();

        // Prompt user to choose pizza size
        System.out.print("Choose pizza size (small, medium, large): ");
        String size = scanner.nextLine();

        // Create a new pizza object
        Pizza pizza = new Pizza(type, size);

        // Display available toppings
        System.out.println("Available toppings: ");
    for (String topping : availableToppings) {
            System.out.println("- " + topping);
        }

        // Prompt user to enter toppings
        System.out.println("Enter your toppings (type 'done' when finished): ");
        while (true) {
            String topping = scanner.nextLine();
            if (topping.equalsIgnoreCase("done")) {
                break; // Exit loop if user is done
            }
            // Check if the topping is available
            boolean isAvailable = false;
            for (String availableTopping : availableToppings) {
                if (availableTopping.equalsIgnoreCase(topping)) {
                    isAvailable = true;
                    break;
                }
            }
            if (isAvailable) {
                pizza.addTopping(topping); // Add topping to the pizza
            } else {
                System.out.println("Topping not available. Please choose another.");
            }
        }

        // Ask for the quantity of the pizza
        System.out.print("How many pizzas of this type would you like to order? ");
        int quantity = scanner.nextInt();

        // Calculate total price for the order
        double totalOrderPrice = pizza.calculateTotalPrice() * quantity;

        // Display the final order summary
        System.out.println("Your Order:");
        System.out.println(pizza);
        System.out.println("Quantity: " + quantity);
        System.out.println("Total Price for " + quantity + " pizzas: $" + String.format("%.2f", totalOrderPrice));

        scanner.close(); // Close the scanner
    }
    }


 #Vector

    import java.util.HashMap;
     import java.util.Scanner;
     import java.util.Vector;

    class Pizza {
    private String type; // Type of the pizza
    private String size; // Size of the pizza
    private Vector<String> toppings; // Vector to store toppings
    private double basePrice; // Base price of the pizza

    // Constructor that initializes the type, size, and base price
    public Pizza(String type, String size) {
        this.type = type;
        this.size = size;
        this.toppings = new Vector<>(); // Initialize the toppings vector
        this.basePrice = calculateBasePrice(type, size); // Calculate base price based on type and size
    }

    // Method to calculate the base price based on the type and size
    private double calculateBasePrice(String type, String size) {
        double typeBasePrice;
        switch (type.toLowerCase()) {
            case "margherita":
                typeBasePrice = 8.00;
                break;
            case "pepperoni":
                typeBasePrice = 9.00;
                break;
            case "veggie":
                typeBasePrice = 8.50;
                break;
            case "bbq chicken":
                typeBasePrice = 10.00;
                break;
            default:
                typeBasePrice = 0.00; // Return 0 if type is invalid
        }

        // Adjust base price based on size
        double sizeMultiplier;
        switch (size.toLowerCase()) {
            case "small":
                sizeMultiplier = 1.0; // No extra charge for small
                break;
            case "medium":
                sizeMultiplier = 1.25; // 25% extra for medium
                break;
            case "large":
                sizeMultiplier = 1.5; // 50% extra for large
                break;
            default:
                sizeMultiplier = 0.0; // Return 0 if size is invalid
        }

        return typeBasePrice * sizeMultiplier; // Calculate total base price
    }

    // Method to add a topping to the pizza
    public void addTopping(String topping) {
        toppings.add(topping); // Add topping to the vector
    }

    // Method to calculate the total price of the pizza
    public double calculateTotalPrice() {
        return basePrice + (toppings.size() * 1.50); // Each topping costs $1.50
    }

    // Override toString method to display pizza details
    @Override
    public String toString() {
        return "Pizza Type: " + type + ", Size: " + size + ", Toppings: " + toppings + ", Total Price: $" + String.format("%.2f", calculateTotalPrice());
    }
    }

    public class PizzaRestaurantv {
    // Map to store available toppings
    private static final HashMap<String, String[]> availableToppings = new HashMap<>();

    // Static block to initialize available toppings
    static {
        availableToppings.put("pepperoni", new String[]{"pepperoni"});
        availableToppings.put("mushrooms", new String[]{"mushrooms"});
        availableToppings.put("onions", new String[]{"onions"});
        availableToppings.put("sausage", new String[]{"sausage"});
        availableToppings.put("bacon", new String[]{"bacon"});
        availableToppings.put("extra cheese", new String[]{"extra cheese"});
        availableToppings.put("black olives", new String[]{"black olives"});
        availableToppings.put("green peppers", new String[]{"green peppers"});
        availableToppings.put("pineapple", new String[]{"pineapple"});
        availableToppings.put("spinach", new String[]{"spinach"});
    }

    // Map to store available pizza types
    private static final String[] availablePizzaTypes = {"Margherita", "Pepperoni", "Veggie", "BBQ Chicken"};

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // Scanner for user input
        System.out.println("Welcome to the Pizza Restaurant!");

        // Prompt user to choose pizza type
        System.out.println("Available pizza types: ");
        for (String pizzaType : availablePizzaTypes) {
            System.out.println("- " + pizzaType);
        }
        System.out.print("Choose pizza type: ");
        String type = scanner.nextLine();

        // Prompt user to choose pizza size
        System .out.print("Choose pizza size (small, medium, large): ");
        String size = scanner.nextLine();

        // Create a new pizza object
        Pizza pizza = new Pizza(type, size);

        // Display available toppings
        System.out.println("Available toppings: ");
        for (String topping : availableToppings.keySet()) {
            System.out.println("- " + topping);
        }

        // Prompt user to enter toppings
        System.out.println("Enter your toppings (type 'done' when finished): ");
        while (true) {
            String topping = scanner.nextLine();
            if (topping.equalsIgnoreCase("done")) {
                break; // Exit loop if user is done
            }
            // Check if the topping is available
            if (availableToppings.containsKey(topping.toLowerCase())) {
                pizza.addTopping(topping); // Add topping to the pizza
            } else {
                System.out.println("Topping not available. Please choose another.");
            }
        }

        // Ask for the quantity of the pizza
        System.out.print("How many pizzas of this type would you like to order? ");
        int quantity = scanner.nextInt();

        // Calculate total price for the order
        double totalOrderPrice = pizza.calculateTotalPrice() * quantity;

        // Display the final order summary
        System.out.println("Your Order:");
        System.out.println(pizza);
        System.out.println("Quantity: " + quantity);
        System.out.println("Total Price for " + quantity + " pizzas: $" + String.format("%.2f", totalOrderPrice));

        scanner.close(); // Close the scanner
    }
    }

  #JDBC
  
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.PreparedStatement;
    import java.sql.SQLException;
    import java.util.Scanner;

    class PizzaParlour {
    private String pizzaType;
    private double basePrice;
    private double toppingPrice;

    public PizzaParlour(String pizzaType, double basePrice) {
        this.pizzaType = pizzaType;
        this.basePrice = basePrice;
        this.toppingPrice = 0;
    }

    public void addTopping(double price) {
        this.toppingPrice += price;
    }

    public double calculateTotal() {
        return basePrice + toppingPrice;
    }

    public void printReceipt() {
        System.out.println("----- Pizza Order -----");
        System.out.printf("Pizza Type: %s ($%.2f)\n", pizzaType, basePrice);
        System.out.printf("Toppings: $%.2f\n", toppingPrice);
        System.out.printf("Total Cost (Pizza + Toppings): $%.2f\n", calculateTotal());
        System.out.println("-----------------------");
    }

    public String getPizzaType() {
        return pizzaType;
    }

    public double getBasePrice() {
        return basePrice;
    }

    public double getToppingPrice() {
        return toppingPrice;
    }

    public double getTotalPrice() {
        return calculateTotal();
    }
    }

    public class PizzaParlourClientSql {
    private static final String DB_URL = "jdbc:mysql://localhost:3307/pizza_parlour";
    private static final String USER = "root";
    private static final String PASS = "";

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Pizza types and their base prices
        String[] pizzaTypes = {"Margherita", "Pepperoni", "Vegetarian", "Supreme"};
        double[] basePrices = {8.99, 10.99, 9.49, 11.49};

        // Toppings and their prices
        String[] toppings = {"Mushrooms", "Olives", "Bell Peppers", "Extra Cheese"};
        double[] toppingPrices = {1.50, 1.25, 1.75, 2.00};

        // Display pizza types
        System.out.println("Welcome to the Pizza Parlour!");
        System.out.println("Choose a pizza type:");

        for (int i = 0; i < pizzaTypes.length; i++) {
            System.out.printf("%d. %s\n", i + 1, pizzaTypes[i]);
        }

        System.out.print("Enter the number of your choice: ");
        int pizzaChoice = scanner.nextInt() - 1;

        if (pizzaChoice < 0 || pizzaChoice >= pizzaTypes.length) {
            System.out.println("Invalid choice. Exiting...");
            return;
        }

        PizzaParlour order = new PizzaParlour(pizzaTypes[pizzaChoice], basePrices[pizzaChoice]);

        // Display toppings
        System.out.println("Select toppings (Enter 0 to finish):");

        for (int i = 0; i < toppings.length; i++) {
            System.out.printf("%d. %s\n", i + 1, toppings[i]);
        }

        boolean addingToppings = true;
        while (addingToppings) {
            System.out.print("Enter the number of your topping choice: ");
            int toppingChoice = scanner.nextInt() - 1;

            if (toppingChoice == -1) {
                addingToppings = false;
            } else if (toppingChoice < 0 || toppingChoice >= toppings.length) {
                System.out.println("Invalid choice. Please try again.");
            } else {
                order.addTopping(toppingPrices[toppingChoice]);
                System.out.println("Added: " + toppings[toppingChoice]);
            }
        }

        // Print receipt
        order.printReceipt();

        // Save order to database
        saveOrderToDatabase(order);

        System.out.println("Thank you for ordering! Enjoy your pizza!");

        scanner.close();
    }

    private static void saveOrderToDatabase(PizzaParlour order) {
        try (Connection conn = DriverManager.getConnection(DB_URL, USER, PASS)) {
            String sql = "INSERT INTO orders (pizza_type, base_price, topping_price, total_price) VALUES (?, ?, ?, ?)";
            try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
                pstmt.setString(1, order.getPizzaType());
                pstmt.setDouble(2, order.getBasePrice());
                pstmt.setDouble(3, order.getToppingPrice());
                pstmt.setDouble(4, order.getTotalPrice());
                pstmt.executeUpdate();
            }
            System.out.println("Order saved to database.");
        } catch (SQLException e) {
            e.printStackTrace();
            System.out.println("Failed to save order to database.");
        }
    }
    }

#GUI

    import javax.swing.*;
    import java.awt.event.ActionEvent;
    import java.awt.event.ActionListener;

    public class PizzaRestaurantGUI {
    private static String[] pizzaTypes = {"Margherita", "Pepperoni", "BBQ Chicken", "Vegetarian"};
    // Prices for Small, Medium, and Large for each pizza type
    private static double[][] pizzaPrices = {
        {8.99, 10.99, 12.99}, // Margherita prices: Small, Medium, Large
        {9.99, 11.99, 13.99}, // Pepperoni prices: Small, Medium, Large
        {10.99, 12.99, 14.99}, // BBQ Chicken prices: Small, Medium, Large
        {7.99, 9.99, 11.99}    // Vegetarian prices: Small, Medium, Large
     };

    public static void main(String[] args) {
        // Create the frame
        JFrame frame = new JFrame("Pizza Restaurant");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 450);
        frame.setLayout(null);

        // Create components
        JLabel titleLabel = new JLabel("Welcome to the Pizza Restaurant!");
        titleLabel.setBounds(50, 10, 300, 20);
        
        JLabel pizzaLabel = new JLabel("Select Pizza Type:");
        pizzaLabel.setBounds(20, 40, 150, 20);
        
        JComboBox<String> pizzaComboBox = new JComboBox<>(pizzaTypes);
        pizzaComboBox.setBounds(180, 40, 150, 20);
        
        JLabel sizeLabel = new JLabel("Size:");
        sizeLabel.setBounds(20, 80, 150, 20);
        
        String[] sizes = {"Small", "Medium", "Large"};
        JComboBox<String> sizeComboBox = new JComboBox<>(sizes);
        sizeComboBox.setBounds(180, 80, 150, 20);
        
        JLabel toppingsLabel = new JLabel("Toppings (comma-separated):");
        toppingsLabel.setBounds(20, 120, 200, 20);
        
        JTextField toppingsField = new JTextField();
        toppingsField.setBounds(20, 150, 310, 20);
        
        JLabel quantityLabel = new JLabel("Quantity:");
        quantityLabel.setBounds(20, 190, 150, 20);
        
        JTextField quantityField = new JTextField();
        quantityField.setBounds(180, 190, 150, 20);
        
        JButton orderButton = new JButton("Place Order");
        orderButton.setBounds(20, 230, 150, 30);
        
        JTextArea outputArea = new JTextArea();
        outputArea.setBounds(20, 270, 350, 80);
        outputArea.setEditable(false);
        
        JLabel billLabel = new JLabel("Total Amount of Bill:");
        billLabel.setBounds(20, 360, 150, 20);
        
        JTextField totalBillField = new JTextField();
        totalBillField.setBounds(180, 360, 150, 20);
        totalBillField.setEditable(false); // Make it read-only
        
        // Add components to the frame
        frame.add(titleLabel);
        frame.add(pizzaLabel);
        frame.add(pizzaComboBox);
        frame.add(sizeLabel);
        frame.add(sizeComboBox);
        frame.add(toppingsLabel);
        frame.add(toppingsField);
        frame.add(quantityLabel);
        frame.add(quantityField);
        frame.add(orderButton);
        frame.add(outputArea);
        frame.add(billLabel);
        frame.add(totalBillField);
        
        // Add action listener to the order button
        orderButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                int pizzaChoice = pizzaComboBox.getSelectedIndex();
                int sizeChoice = sizeComboBox.getSelectedIndex(); // 0 for Small, 1 for Medium, 2 for Large
                String size = (String) sizeComboBox.getSelectedItem();
                String toppings = toppingsField.getText();
                int quantity;

                try {
                    quantity = Integer.parseInt(quantityField.getText());
                    double totalPrice = pizzaPrices[pizzaChoice][sizeChoice] * quantity;

                    // Display order summary
                    String orderSummary = "Order Summary:\n" +
                            "Pizza Type: " + pizzaTypes[pizzaChoice] + "\n" +
                            "Size: " + size + "\n" +
                            "Toppings: " + toppings + "\n" +
                            "Quantity: " + quantity + "\n";
                    outputArea.setText(orderSummary);
                    
                    // Display total amount in the separate field
                    totalBillField.setText(String.format("$%.2f", totalPrice));
                } catch (NumberFormatException ex) {
                    outputArea.setText("Error: Please enter a valid quantity.");
                    totalBillField.setText(""); // Clear the total bill field on error
                }
            }
        });

        // Set frame visibility
        frame.setVisible(true);
    }
    }


  
