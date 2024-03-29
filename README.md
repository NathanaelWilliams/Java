# Java 
A number of samples of Java programs
## Sample1 ##
```java
import java.util.*;

public class CalculatePi {
    public static void main(String[] args) {
        double pi = 0.0;
        int terms = 1000000000; //Max
        for (int i = 0; i < terms; i++) {
            pi += Math.pow(-1, i) / (2 * i + 1);
        }
        pi *= 4;
        System.out.println("_PI_ is :" + pi);
    }
}
```
**Attention**.1000000000 is `MAX`
## Sample2 ##
```java
import java.util.Scanner;

public class PrimeNumberChecker {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("scan num：");
        int number = scanner.nextInt();

        if (isPrime(number)) {
            System.out.println(number + " yes");
        } else {
            System.out.println(number + " no");
        }

        scanner.close();
    }

    public static boolean isPrime(int num) {
        if (num <= 1) {
            return false; 
        }
        if (num == 2) {
            return true; 
        }
        if (num % 2 == 0) {
            return false; 
        }
        for (int i = 3; i <= Math.sqrt(num); i += 2) {
            if (num % i == 0) {
                return false; 
            }
        }
        return true; 
    }
}
```
## Sample3 ##
```java
import java.util.Scanner;

public class CircleCalculator {

    public static void main(String[] args) {
        // Create a Scanner object to read user input
        Scanner scanner = new Scanner(System.in);

        // Prompt the user to enter the radius of the circle
        System.out.print("Enter the radius of the circle: ");
        double radius = scanner.nextDouble();

        // Calculate the circumference and area of the circle
        double circumference = calculateCircumference(radius);
        double circleArea = calculateArea(radius);

        // Calculate the area of the inscribed equilateral triangle
        double triangleArea = calculateInscribedTriangleArea(radius);

        // Display the results
        System.out.println("The circumference of the circle is: " + circumference);
        System.out.println("The area of the circle is: " + circleArea);
        System.out.println("The area of the inscribed equilateral triangle is: " + triangleArea);

        // Close the scanner
        scanner.close();
    }

    /**
     * Calculates the circumference of a circle.
     *
     * @param radius The radius of the circle.
     * @return The circumference of the circle.
     */
    public static double calculateCircumference(double radius) {
        return 2 * Math.PI * radius;
    }

    /**
     * Calculates the area of a circle.
     *
     * @param radius The radius of the circle.
     * @return The area of the circle.
     */
    public static double calculateArea(double radius) {
        return Math.PI * radius * radius;
    }

    /**
     * Calculates the area of an inscribed equilateral triangle in a circle.
     *
     * @param radius The radius of the circle.
     * @return The area of the inscribed equilateral triangle.
     */
    public static double calculateInscribedTriangleArea(double radius) {
        return (Math.sqrt(3) / 4) * radius * radius;
    }
}
```
## Sample4 ##
```java
import java.math.BigDecimal;
import java.util.Scanner;
import java.math.MathContext;

public class NumberCalculations {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter a number: ");
        double number = scanner.nextDouble();

        // Calculate the square root
        double squareRoot = Math.sqrt(number);
        System.out.println("Square root: " + squareRoot);

        // Calculate the square
        double square = number * number;
        System.out.println("Square: " + square);

        // Calculate the opposite number
        double oppositeNumber = -number;
        System.out.println("Opposite number: " + oppositeNumber);

        // Calculate the reciprocal (BigDecimal is used for precision)
        BigDecimal bdNumber = new BigDecimal(number);
        BigDecimal reciprocal = BigDecimal.ONE.divide(bdNumber, MathContext.DECIMAL64);
        System.out.println("Reciprocal: " + reciprocal);

        // Calculate the sine, cosine, tangent, and cotangent
        double sine = Math.sin(number);
        System.out.println("Sine: " + sine);

        double cosine = Math.cos(number);
        System.out.println("Cosine: " + cosine);

        double tangent = Math.tan(number);
        System.out.println("Tangent: " + tangent);

        // Cotangent is the reciprocal of the tangent
        double cotangent = 1 / Math.tan(number);
        System.out.println("Cotangent: " + cotangent);

        scanner.close();
    }
}
```
**Attention**.Note: Since the tangent function is not defined at integer multiples of π/2 and - π/2, the calculation of tangent and cotangent will be problematic if the input values are these points. In addition, for input values that are very close to these points, the calculation results may also be inaccurate due to the precision limitations of floating point numbers.
## Sample5 ##
```java
import java.util.Scanner;
import java.util.HashSet;
import java.util.Set;

public class TwentyFourGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter a four-digit number: ");
        int number = scanner.nextInt();
        scanner.close();

        if (number < 1000 || number > 9999) {
            System.out.println("Please enter a valid four-digit number.");
            return;
        }

        int[] digits = new int[4];
        for (int i = 3; i >= 0; i--) {
            digits[3 - i] = number % 10;
            number /= 10;
        }

        if (solve24(digits)) {
            System.out.println("Solution found:");
            for (String solution : solutions) {
                System.out.println(solution);
            }
        } else {
            System.out.println("No Solution");
        }
    }

    private static Set<String> solutions = new HashSet<>();
    private static boolean solve24(int[] digits) {
        solutions.clear();
        return solve24Helper(digits, 0, 0, "");
    }

    private static boolean solve24Helper(int[] digits, double current, double last, String expression) {
        if (digits.length == 0) {
            if (current == 24) {
                solutions.add(expression);
                return true;
            }
            return false;
        }

        for (int i = 0; i < digits.length; i++) {
            int[] remaining = new int[digits.length - 1];
            System.arraycopy(digits, 0, remaining, 0, i);
            System.arraycopy(digits, i + 1, remaining, i, digits.length - i - 1);

            if (i == 0 || last != digits[i]) {
                if (solve24Helper(remaining, current + digits[i], digits[i], expression + "+" + digits[i])) return true;
                if (solve24Helper(remaining, current - digits[i], digits[i], expression + "-" + digits[i])) return true;
                if (solve24Helper(remaining, current * digits[i], digits[i], expression + "*" + digits[i])) return true;
                if (digits[i] != 0 && solve24Helper(remaining, current / digits[i], digits[i], expression + "/" + digits[i])) return true;
            }
        }

        return false;
    }
}
```
**Attention**.This program uses a recursive function, `Solve24Helper`, to try all possible combinations. It uses a `HashSet` to store all found solutions to avoid duplication. The program first checks to see if the input is a valid four-digit number, and then breaks the number down into individual digits. It then calls the `solve24` function to try to find a solution.

## Sample6 ##
```java
import java.util.*;
public class SnakeGame {
    private int width;
    private int height;
    private int[][] board;
    private int[] snake;
    private int[] food;
    private int score;
    private boolean gameOver;

    // Initialize the game
    public SnakeGame(int width, int height) {
        this.width = width;
        this.height = height;
        this.board = new int[width][height];
        this.snake = new int[]{width / 2, height / 2}; // Start at the center
        this.food = generateFood();
        this.score = 0;
        this.gameOver = false;
    }

    // Generate a new food position
    private int[] generateFood() {
        int x, y;
        do {
            x = (int) (Math.random() * width);
            y = (int) (Math.random() * height);
        } while (board[x][y] != 0);
        return new int[]{x, y};
    }

    // Move the snake
    private void move(int dx, int dy) {
        int newX = snake[0] + dx;
        int newY = snake[1] + dy;

        // Check for game over conditions
        if (newX < 0 || newX >= width || newY < 0 || newY >= height || board[newX][newY] < 0) {
            gameOver = true;
            return;
        }

        // Update the snake's position
        snake[0] = newX;
        snake[1] = newY;

        // Check if the snake has eaten the food
        if (newX == food[0] && newY == food[1]) {
            score++;
            food = generateFood();
        } else {
            // Move the rest of the snake body
            for (int i = score; i > 0; i--) {
                board[snake[i * 2]][snake[i * 2 + 1]] = i;
            }
        }

        board[newX][newY] = -1; // Snake head
    }

    // Render the game board
    private void render() {
        for (int y = 0; y < height; y++) {
            for (int x = 0; x < width; x++) {
                if (x == snake[0] && y == snake[1]) {
                    System.out.print("O "); // Snake head
                } else if (x == food[0] && y == food[1]) {
                    System.out.print("X "); // Food
                } else if (board[x][y] > 0) {
                    System.out.print("o "); // Snake body
                } else {
                    System.out.print(". ");
                }
            }
            System.out.println();
        }
        System.out.println("Score: " + score);
    }

    // Main game loop
    public void run() {
        Scanner scanner = new Scanner(System.in);
        while (!gameOver) {
            render();
            System.out.print("Enter direction (WASD): ");
            String input = scanner.nextLine().toUpperCase();
            switch (input) {
                case "W":
                    move(0, -1);
                    break;
                case "A":
                    move(-1, 0);
                    break;
                case "S":
                    move(0, 1);
                    break;
                case "D":
                    move(1, 0);
                    break;
                default:
                    System.out.println("Invalid direction.");
                    continue;
            }
            if (gameOver) {
                System.out.println("Game Over! Final score: " + score);
            }
        }
        scanner.close();
    }

    public static void main(String[] args) {
        SnakeGame game = new SnakeGame(20, 20);
        game.run();
    }
}
```

**Attention**. In this program, we created a `SnakeGame` class that handles the game logic. The game is represented in a two-dimensional array `board`, where `-1` represents the snake's head, `0` represents a space, and a positive integer represents the snake's body part. We use the snake array to track the position of the `snake`, and the `food`array to track the position of the food.
<br>
<br>

The user controls the movement of the snake via console input (on W, a left, S down, D Right). After each move, the program checks to see if the game is over (for example, if the snake hit a wall or ate itself). If the game is not finished, the program updates the location of the snake and food, and rerenders the game board.
<br>
<br>

To run this program, copy it into the Java development environment and run the `main` method. The game will start on the console and you can control the snake's movement by entering the `WASD`(cant be wasd) key.

## Sample7 ##
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.math.BigDecimal;
import java.math.MathContext;
import java.util.Scanner;

public class WritePiToFile {
    public static void main(String[] args) {
        // Create a Scanner object to read user input
        Scanner scanner = new Scanner(System.in);

        // Prompt the user to enter the directory to write the file
        System.out.print("Enter the directory to write the file: ");
        String directory = scanner.nextLine();

        // Prompt the user to enter the file name
        System.out.print("Enter the file name: ");
        String fileName = scanner.nextLine();

        // Close the scanner as we no longer need to read input
        scanner.close();

        // Create the full file path
        String filePath = directory + "/" + fileName;

        // Calculate Pi with a precision of 100 digits after the decimal point
        BigDecimal pi = new BigDecimal(Math.PI);
        MathContext mc = new MathContext(102); // 100 digits precision plus 2 for "3."
        pi = pi.round(mc);

        // Write Pi to the file
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            writer.write(pi.toString().substring(0, 102)); // Write the first 102 characters (100 digits + "3.")
            System.out.println("Pi has been written to " + filePath);
        } catch (IOException e) {
            System.err.println("An error occurred while writing to the file: " + e.getMessage());
        }
    }
}
```
**Attention**.In this program, we first create a `Scanner` object to read the file directory and file name entered by the user. Then, we closed the `Scanner` object because we no longer needed to read the input. Next, we used the `BigDecimal` class and the `MathContext` object to calculate the pi and set the required precision. Finally, we use the `BufferedWriter` and `FileWriter` to write the first `100 bits` of pi to a file.
<br>
<br>
To run this program, copy it into the Java development environment and run the `main` method. The program prompts you for a file directory and file name, then creates a new file under that directory and writes the first 100 digits of pi to the file.
## Sample8 ##
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class SimpleWebCrawler {

    public static void main(String[] args) {
        String startingUrl = "http://example.com"; // Replace with the URL you want to start crawling
        crawl(startingUrl);
    }

    private static void crawl(String url) {
        try {
            // Create a URL object
            URL siteURL = new URL(url);

            // Open the connection
            HttpURLConnection connection = (HttpURLConnection) siteURL.openConnection();

            // Connect to the site
            connection.connect();

            // Check if the response code is OK
            if (connection.getResponseCode() == 200) {
                // Read the input stream
                BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));

                String line;
                while ((line = reader.readLine()) != null) {
                    if (line.contains("href=\"")) {
                        // Extract the link
                        int start = line.indexOf("href=\"") + 6;
                        int end = line.indexOf("\"", start);
                        String link = line.substring(start, end);

                        // Print the link
                        System.out.println(link);
                    }
                }
                reader.close();
            }

            // Disconnect
            connection.disconnect();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
**Attention**.Please note that web crawling should be done responsibly. Always check the `robots.txt` file of a website and respect its policies. Additionally, make sure not to overload the website’s server by making too many requests in a short period of time.
<br><br>
In this example, we use Java’s `HttpURLConnection` class to connect to a webpage and read its contents. We then search for lines that contain the “href="” string, which indicates the start of a link. We extract the link and print it.
<br><br>

This is a very basic example and does not handle various complexities such as relative URLs, redirections, or different types of links (like `javascript`: links). It also does not crawl recursively to follow the extracted links.
## Sample9 ##
```java
public class HeartPattern {
    public static void main(String[] args) {
        int i, j;
        int n = 10; // You can change the size of the heart

        // Upper part of the heart
        for (i = n / 2; i <= n; i += 2) {
            // Print spaces
            for (j = 1; j < n - i; j += 2) {
                System.out.print(" ");
            }

            // Print stars
            for (j = 1; j <= i; j++) {
                System.out.print("*");
            }

            // Print spaces between the two upper lobes of the heart
            for (j = 1; j <= n - i; j++) {
                System.out.print(" ");
            }

            // Print stars
            for (j = 1; j <= i; j++) {
                System.out.print("*");
            }

            System.out.println();
        }

        // Lower part of the heart
        for (i = n; i >= 1; i--) {
            // Print stars
            for (j = i; j < n; j++) {
                System.out.print("*");
            }

            // Print space in the middle of the heart
            for (j = 1; j <= 2 * i - 1; j++) {
                System.out.print(" ");
            }

            // Print stars
            for (j = i; j < n; j++) {
                System.out.print("*");
            }

            System.out.println();
        }
    }
}
```
**Attention**.The program uses two nested for loops to print the heart. The outer loop controls the number of rows, and the inner loop controls the spaces and asterisks in each row. The program prints first the top half of the heart, then the bottom half.