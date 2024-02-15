# Java
A number of samples of Java programs
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