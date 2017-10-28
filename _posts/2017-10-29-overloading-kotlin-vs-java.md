---
layout: post
title: "Kotlin vs Java"
---

Naujos JVM (Java Virtual Machine) programavimo kalbos Kotlin apžvalga ir palyginimas su Java.

## Kotlin vs Java
**Turinys**
- [Overloaded methods](#overloaded-methods) 
- [FIltered collections](#filter-collections) 

### Overloaded methods


```java
package overloadedMethods;

public class OverloadedMethodJava {
    void printMessage(String message){ 
      System.out.printf("Message: %s\n", message); 
    }
    void printMessage(String message, String prefix){ 
      System.out.printf("Message: %s, Prefix: %s\n", message, prefix); 
    }
    void printMessage(String message, String prefix, String suffix){ 
      System.out.printf("Message: %s, Prefix: %s, Suffix: %s\n", message, prefix, suffix); 
    }

    public static void main(String[] args) {
        new OverloadedMethodJava().printMessage("Hello");
        new OverloadedMethodJava().printMessage("Hello", "WithPRefix");
        new OverloadedMethodJava().printMessage("Hello", "WithPRefix", "AndSuffix");
    }
}
//--------------------------------------------Java-----------------------------------------------//
```



```kotlin
package overloadedMethods

class OverloadedMethodKotlin {
    fun printMessage(message: String, prefix: String = "", suffix: String = "") {
        println("$message $prefix $suffix")
    }
}
fun main(args: Array<String>) {
    val overloaded = OverloadedMethodKotlin() // Immutable readonly
    overloaded.printMessage("Hi im Kotlin")
    overloaded.printMessage("Hi im Kotlin", "with prefix")
    overloaded.printMessage("Hi im Kotlin", "with prefix", "AndSuffix")
    // Bet kokia tvarka pagal vardą parametro
    overloaded.printMessage(prefix = "Hello im Prefix", message = "im Kotlin", suffix = "And Suffix")

//--------------------------------------------Kotlin-----------------------------------------------//
```

### Filter collections


```java
public class ListExamples {
    public static void main(String[] args) {
        List<Customer> customers = new ArrayList<>(List.of(
                new Customer("Petras"),
                new Customer("Ona"),
                new Customer("Birute")
        ));
        customers.add(new Customer("Petras"));
        System.out.println("----------------------------");
        customers.forEach(System.out::print);
        IntStream intStream = IntStream.range(1, 100);
        intStream.filter(v -> v < 100)
                .mapToDouble(v -> v % 20)
                .forEach(System.out::print);
    }
}
//--------------------------------------------Java-----------------------------------------------//
```


```kotlin
package listOfNumbers
// In JAVA CUSTOMER CLASS AROUND 100 lines with basic methods:)
data class Customer(val name: String)
fun main(args: Array<String>) {
    val customers = ArrayList<Customer>(listOf<Customer>(
            Customer("Petras"),
            Customer("Jonas"),
            Customer("Jonas")
    ))
    customers.add(Customer("Ona"))
    println("--------------------------------")
    customers.forEach { print(" " + it.name) }

    // number 1 to 100 similar to IntStream in JAVA
    val numbers = 1..100
    numbers.filter { it < 100 }
            .map { it % 20 }
            .forEach { print(" " + it) }
}
//--------------------------------------------Kotlin-----------------------------------------------//
```








[Link to another page: HomePage]({{ site.baseurl }}/index).


