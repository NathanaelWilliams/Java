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