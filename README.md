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