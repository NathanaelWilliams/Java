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